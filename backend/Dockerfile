# ---------- Stage 1: Build ----------
FROM golang:1.25-alpine AS builder

WORKDIR /app

# Copy dependency files first
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy source code
COPY . .

# Build binary
RUN CGO_ENABLED=0 GOOS=linux go build -o skillpulse .

# ---------- Stage 2: Runtime ----------
FROM alpine:3.23

RUN apk --no-cache add ca-certificates wget

WORKDIR /app

COPY --from=builder /app/skillpulse .

EXPOSE 8080

CMD ["./skillpulse"]