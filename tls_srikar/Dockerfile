# Multi-stage build for C++ banking system

# Stage 1: Builder
FROM gcc:latest AS builder

WORKDIR /build

# Copy the C++ source file
COPY c++_fixed /build/bank.cpp

# Compile the C++ program
RUN g++ -std=c++17 -o bank bank.cpp -lm

# Stage 2: Runtime
FROM alpine:latest

WORKDIR /app

# Install runtime dependencies (glibc for compiled binary)
RUN apk add --no-cache libc6-compat libgcc libstdc++

# Copy the compiled binary from builder stage
COPY --from=builder /build/bank /app/bank

# Run the program
ENTRYPOINT ["/app/bank"]
