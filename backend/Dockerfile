#STAGE1 
FROM golang:1.24 as builder

#Setting the Current Working Directory inside the container
WORKDIR /app

#Copying the go.mod and go.sum files to the working directory
COPY go.mod go.sum ./

#to download all the dependencies(libraries) of the project
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o server .

#stage2 
FROM golang:1.24-alpine

#Setting the Current Working Directory inside the container
WORKDIR /app

#Copying the Pre-built binary file from the previous stage
COPY --from=builder /app/server /app/server

EXPOSE 8080

CMD ["/app/server"]