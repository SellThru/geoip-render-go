# geoip-render-go
Golang project for looking up geo from an IP. Meant to be deployed on Render.

## Routes

`/geo/point` takes `ip` as a query parameter and returns the lat/long for that location:

```json
{
  "point": [<LAT>,<LON>]
}
```

`/geo/zip` takes `ip` as a query parameter and returns the zip for that location:

```json
{
  "zip": "85004"
}
```

## Dependencies

In order to use this project, you'll need a copy of your own [Maxmind GeoIP database](https://www.maxmind.com/en/geoip2-services-and-databases). You can sign up for the GeoLite2 database [here](https://www.maxmind.com/en/geolite2/signup?lang=en).

This project then relies on the [oschwald/geoip2-golang](https://pkg.go.dev/github.com/oschwald/geoip2-golang) package for looking up an IP in a MaxMind GeoIP database. See the documentation for all of the queries that can be made and the resulting structs.

## Environment variables

This project relies on the following environment variables:

| ENV Variable | Description                                                                | Required | Default   |
|--------------|----------------------------------------------------------------------------|----------|-----------|
| `GEO_FILE`   | The location of your Maxmind GeoIP database (e.g., `./GeoLite2-City.mmdb`) | Yes      | None      |
| `MODE`       | The mode to launch the application in.                                     | No      | "release" |
| `PORT`       | The port for the web service to listen on.                                 | No      | 3000      |


## Notes

- This project DOES NOT log web requests. It only prints status logs. If you want to log each request, you can add it to the Go Gin logger.
