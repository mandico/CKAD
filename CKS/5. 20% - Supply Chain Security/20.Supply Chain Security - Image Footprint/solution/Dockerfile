# build container stage 1
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y golang-go
COPY app.go .
RUN CGO_ENABLED=0 go build app.go

# app container stage 2
# Specific package version.
FROM alpine:3.19.1
# No use root
RUN addgroup -S appgroup && adduser -S appuser -G appgroup -h /home/appuser
# Filesystem read only.
RUN chmod a-w /etc
# No shell access.
RUN rm -rf /bin/*
COPY --from=0 /app .
USER appuser
CMD ["./app"]