FROM caddy:2.4.5-windowsservercore-1809 as base
FROM mcr.microsoft.com/windows/nanoserver:1809 as server

COPY --from=base ["/Windows/System32/netapi32.dll", "/Windows/System32"]
RUN mkdir \config;
RUN mkdir \data;
RUN mkdir \etc\caddy; mkdir \usr\share\caddy;

COPY --from=base ["/caddy.exe", "/"]
COPY --from=base ["/etc/caddy/Caddyfile", "/etc/caddy/"]
COPY --from=base ["/usr/share/caddy/index.html", "/usr/share/caddy/"]

# See https://caddyserver.com/docs/conventions#file-locations for details
ENV XDG_CONFIG_HOME c:/config
ENV XDG_DATA_HOME c:/data

LABEL MAINTAINER SiritasDho<dahoba@gmail.com>
LABEL org.opencontainers.image.source="https://github.com/dahoba/caddyserver"

EXPOSE 80 443 2019

# Make sure it runs and reports its version
RUN ["caddy", "version"]

CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]
