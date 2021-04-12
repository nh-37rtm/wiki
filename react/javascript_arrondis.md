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
function calcHours(selfControl) {
        if (selfChanges) {
            return;
        }
        try {
            selfChanges = true
            // reccupere les éléments
            var calcPlaceHolder = $(selfControl).parents(".hours-calc-placeholder");
            var beginDateElement = calcPlaceHolder.find(".hours-calc-begin-date");
            var endDateElement = calcPlaceHolder.find(".hours-calc-end-date");
            var hoursRoundedElement = calcPlaceHolder.find(".hours-calc-hours");

            var beginDateAsString = beginDateElement.first().val();
            var EndDateAsString = endDateElement.first().val();

            var beginTs = Date.parse(beginDateAsString);
            var endTs = Date.parse(EndDateAsString);

            // fait les arrondis
            var halfHoursRounded = Math.round((endTs - beginTs) / 1000 / 60 / 30);
            var hoursRounded = halfHoursRounded / 2;
            var endRounded = new Date(beginTs + (hoursRounded * 60 * 60 * 1000));
            var timeZoneOffset = new Date(endRounded).getTimezoneOffset() * 60 * 1000;
            var timeZoneWithOffset = new Date(beginTs + (hoursRounded * 60 * 60 * 1000) - timeZoneOffset);
            var endIsoRounder = endRounded;

            // Joue avec les offsets pour éviter l'erreur de conversion GMT en Local
            var isoString = timeZoneWithOffset.toISOString();
            endDateElement.get(0).value = isoString.substr(0, isoString.length - 1); // Remove the Z Zulu ending
            endDateElement.get(0).dispatchEvent(new Event('change'));
            hoursRoundedElement.get(0).value = hoursRounded;
        } finally {
            selfChanges = false
        }
    }
````