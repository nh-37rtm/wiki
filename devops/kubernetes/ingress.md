# nginx ingress

to customize ingress for only current location you can add for exemple

````yaml
nginx.ingress.kubernetes.io/x-forwarded-prefix: "/xperience-v2-front"
    nginx.ingress.kubernetes.io/configuration-snippet: |
      try_files $uri $uri/ /index.html =404; 
````