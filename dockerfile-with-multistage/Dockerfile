# BUILD ENVIRONMENT
FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY . .

RUN CGO_ENABLED=0 go build -o /app .

# RUNTIME ENVIRONMENT
FROM scratch

# Copy the artifacts from the build stage
COPY --from=build /app /app

# Set the entrypoint for the container
ENTRYPOINT ["/app"]