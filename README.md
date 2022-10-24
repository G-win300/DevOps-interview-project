# DevOps-test-project

Helm chart deploying two application containers: a frontend made with Vue JS and its backend made with nodeJS into AWS kubernetes cluster

This simple application on the click of a button fetches the current time from the backend api server and displays it in the frontend
technologies used includes: 
1. Docker, 
2. Helm, 
3. kubernetes, 
4. AWS Application load balancer

How the ingress file looks

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myingress
  annotations:
    # kubernetes.io/ingress.class: "nginx"
    # nginx.ingress.kubernetes.io/use-regex: "true"
    kubernetes.io/ingress.class: "alb"
    alb.ingress.kubernetes.io/scheme: internet-facing
    
    # Health Check Settings
    alb.ingress.kubernetes.io/healthcheck-protocol: HTTP 
    alb.ingress.kubernetes.io/healthcheck-port: traffic-port
    alb.ingress.kubernetes.io/healthcheck-interval-seconds: '15'
    alb.ingress.kubernetes.io/healthcheck-timeout-seconds: '5'
    alb.ingress.kubernetes.io/success-codes: '200'
    alb.ingress.kubernetes.io/healthy-threshold-count: '2'
    alb.ingress.kubernetes.io/unhealthy-threshold-count: '2'
    alb.ingress.kubernetes.io/target-type: 'ip'
    
    # External DNS - For creating a Record Set in Route53
    external-dns.alpha.kubernetes.io/hostname: kube.devopsapp.cloud  
    
spec:
  ingressClassName: myapp-ingress-class
  defaultBackend: 
    service: 
      name: frontend
      port:
        number: 80
  rules:
    - host: kube.devopsapp.cloud
      http:
        paths:
          - path: /backend
            pathType: ImplementationSpecific
            backend:
              service:
                name: api
                port:
                  number: 80
                  
          - path: /frontend
            pathType: ImplementationSpecific
            backend:
              service:
                name: frontend
                port:
                  number: 80

```

---

**STEP:** the output of the frontend when accessed at **kube.devopsapp.cloud/frontend** will produce
![frontend](img/frontend.png)

---
**STEP:** the output of the backend when accessed at **kube.devopsapp.cloud/backend** will produce
![backend](img/backend.png)


images used can be seen in my dockerhub:
1. gwin300/frontend1
2. gwin300/backend_api
