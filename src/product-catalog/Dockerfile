#Layer1: Build the application
FROM golang:1.22-alpine as builder

WORKDIR /usr/src/app

COPY . .

RUN go mod download

RUN go build -o product-catalog .

#Layer2: Release the application
FROM alpine as release

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/product-catalog ./

COPY ./products ./products

ENV PRODUCT_CATALOG_PORT=8088

EXPOSE ${PRODUCT_CATALOG_PORT}

ENTRYPOINT [ "./product-catalog" ]