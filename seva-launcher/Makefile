ARCH ?= $(shell uname -m)

ifeq ($(ARCH),x86_64)
	GOARCH=amd64
else ifeq ($(ARCH),aarch64)
	GOARCH=arm64
else
	@echo Unsupported architecture
endif

seva-launcher: web $(shell find . -name '*.go')
	GOARCH=$(GOARCH) go build -tags netgo .

web: $(shell find ../seva-web/build/${SOC}/web)
	rm -rf web
	cp -r ../seva-web/build/${SOC}/web .

.PHONY: all clean run
all: seva-launcher
clean:
	rm -f seva-launcher
	rm -rf web

run: seva-launcher
	@command -v docker-compose >/dev/null 2>&1 || { echo "Error: docker-compose is not installed. Please install docker-compose first."; exit 1; }
	./seva-launcher
