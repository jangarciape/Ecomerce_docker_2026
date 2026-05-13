FROM eclipse-temurin:17-jdk-jammy

# Configuración de la aplicación
ENV APP_HOME=/encomerce-app

# Crear directorio de trabajo
RUN mkdir -p $APP_HOME

WORKDIR $APP_HOME

# Puerto a exponer
EXPOSE 8084

# Copiar el JAR generado
COPY target/encomerce-*.jar app.jar

# Instalar curl para HEALTHCHECK
RUN apt-get update && apt-get install -y curl

# Usuario no root
RUN useradd -m appuser && chown -R appuser:appuser $APP_HOME

USER appuser

# Healthcheck
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost:8084/actuator/health || exit 1

# Comando de inicio
ENTRYPOINT ["java", "-jar", "app.jar"]