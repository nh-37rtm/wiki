---
title: Untitled Page
description: This is the short description
published: true
date: 2021-04-12T14:59:10.150Z
tags: 
editor: undefined
dateCreated: 2021-04-12T14:59:10.150Z
---
# arrondis à la demis heure en javascript


````javascript
function calcHours(selfControl, mode) {
        if (selfChanges) {
            return;
        }
        try {
            selfChanges = true

            // get elements
            var calcPlaceHolder = $(selfControl).parents(".hours-calc-placeholder").first();
            var beginDateElement = calcPlaceHolder.find(".hours-calc-begin-date");
            var endDateElement = calcPlaceHolder.find(".hours-calc-end-date");
            var hoursRoundedElement = calcPlaceHolder.find(".hours-calc-hours");
            var beginDateAsString = beginDateElement.first().val();
            var EndDateAsString = endDateElement.first().val();

            // parse as TS
            var beginTs = Date.parse(beginDateAsString);
            var endTs = Date.parse(EndDateAsString);

            var hoursRounded = 0;

            if (mode == 0) {
                // diff and round by excess (hour ceil)
                hoursRounded = Math.ceil((endTs - beginTs) / 1000 / 60 / 60);
                var endRounded = new Date(beginTs + (hoursRounded * 60 * 60 * 1000));
            } else if (mode == 1) {
                // diff and round by excess (minute round)
                minutesRounded = Math.round((endTs - beginTs) / 1000 / 60);
                hoursRounded = (minutesRounded / 60).toFixed(2);
                var endRounded = new Date(beginTs + (hoursRounded * 60 * 60 * 1000));
            } else {
                cLog("unknown mode !");
            }

            // play with offset to avoid a convertion problem
            var timeZoneOffset = new Date(endRounded).getTimezoneOffset() * 60 * 1000;
            var timeZoneWithOffset = new Date(beginTs + (hoursRounded * 60 * 60 * 1000) - timeZoneOffset);
            var endIsoRounder = endRounded;
            var isoString = timeZoneWithOffset.toISOString();

            endDateElement.get(0).value = isoString.substr(0, isoString.length - 1); // Remove the Z Zulu ending

            endDateElement.get(0).dispatchEvent(new Event('change'));
            hoursRoundedElement.get(0).value = hoursRounded;
        } finally {
            selfChanges = false
        }
    }
````