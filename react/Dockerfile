FROM golang
RUN curl -sSL https://github.com/openfaas/faas/releases/download/0.8.0/fwatchdog > /usr/bin/fwatchdog \
    && chmod +x /usr/bin/fwatchdog 
    
RUN go get -u github.com/ops2go/faas/react \
    && go get -u github.com/gin-gonic/gin \
    && go get -u github.com/gin-gonic/contrib/static \
    && go get -u github.com/auth0/go-jwt-middleware \
    && go get -u github.com/dgrijalva/jwt-go

WORKDIR /go
    
ENV AUTH0_API_CLIENT_SECRET=""
ENV AUTH0_CLIENT_ID=""
ENV AUTH0_DOMAIN="yourdomain.auth0.com"
ENV AUTH0_API_AUDIENCE=""

# Populate example here - i.e. "cat", "sha512sum" or "node index.js"
ENV fprocess="main.go"
# Set to true to see request in function logs
ENV write_debug="false"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1
CMD [ "fwatchdog" ]
