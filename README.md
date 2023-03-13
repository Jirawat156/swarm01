# Ref 
- https://github.com/docker/awesome-compose/tree/master/plex

# url (plex)
- https://jirawatjp.xops.ipv9.xyz

### code compose ใน xOps.ipv9
               version: '3.3' 
               services:
                web: 
               image: jirawatjp/plex:v2
    networks: 
    - webproxy 
    logging:
      driver: json-file
    container_name: jirawatjp
    deploy: 
      replicas: 1 
      labels: 
        - traefik.docker.network=webproxy
        - traefik.enable=true
        - traefik.http.routers.jirawatjp-https.entrypoints=websecure 
        - traefik.http.routers.jirawatjp-https.rule=Host("jirawatjp.xops.ipv9.xyz")
        - traefik.http.routers.jirawatjp-https.tls.certresolver=default
        - traefik.http.services.jirawatjp.loadbalancer.server.port=32400
      resources: 
        reservations: 
          cpus: '0.1'
          memory: 10M
        limits: 
          cpus: '0.4'
          memory: 180M
networks: 
  webproxy: 
    external: true
              
