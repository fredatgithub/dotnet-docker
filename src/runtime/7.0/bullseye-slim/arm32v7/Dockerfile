ARG REPO=mcr.microsoft.com/dotnet/runtime-deps

# Installer image
FROM arm32v7/buildpack-deps:bullseye-curl AS installer

# Retrieve .NET Runtime
RUN dotnet_version=7.0.19 \
    && curl -fSL --output dotnet.tar.gz https://dotnetcli.azureedge.net/dotnet/Runtime/$dotnet_version/dotnet-runtime-$dotnet_version-linux-arm.tar.gz \
    && dotnet_sha512='cb99b6e971077ca5a3c580c04e152026fc2c7430cbb30cc4bd074fa98dcbe1ade684a8267360c0d74e1d72c67622d6106ecb42ff6b1b226f39ff9c2d2f6f0a94' \
    && echo "$dotnet_sha512  dotnet.tar.gz" | sha512sum -c - \
    && mkdir -p /dotnet \
    && tar -oxzf dotnet.tar.gz -C /dotnet \
    && rm dotnet.tar.gz


# .NET runtime image
FROM $REPO:7.0.19-bullseye-slim-arm32v7

# .NET Runtime version
ENV DOTNET_VERSION=7.0.19

COPY --from=installer ["/dotnet", "/usr/share/dotnet"]

RUN ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet
