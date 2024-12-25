FROM bitnami/keycloak:23.0.3-debian-11-r0 as builder

# COPY ./target/*.jar /opt/bitnami/keycloak/providers/
# COPY ./imports /opt/bitnami/keycloak/data/import/

ENV KC_HEALTH_ENABLED=true
ENV KC_METRICS_ENABLED=true
ENV KC_FEATURES=token-exchange
ENV KC_DB=mysql
ENV PROXY_ADDRESS_FORWARDING=true
## Install custom providers
#RUN curl -sL https://github.com/aerogear/keycloak-metrics-spi/releases/download/2.5.3/keycloak-metrics-spi-2.5.3.jar -o /opt/bitnami/keycloak/providers/keycloak-metrics-spi-2.5.3.jar
RUN /opt/bitnami/keycloak/bin/kc.sh build

FROM bitnami/keycloak:23.0.3-debian-11-r0
COPY --from=builder /opt/bitnami/keycloak/ /opt/bitnami/keycloak/
WORKDIR /opt/bitnami/keycloak

# for demonstration purposes only, please make sure to use proper certificates in production instead
# change these values to point to a running postgres instance

ENTRYPOINT ["/opt/bitnami/keycloak/bin/kc.sh","start-dev"]
#ENTRYPOINT ["/opt/keycloak/bin/kc.sh","start-dev", "--auto-build", "--features=preview" ,"--import-realm"]
