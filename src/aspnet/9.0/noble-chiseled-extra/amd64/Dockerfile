ARG REPO=mcr.microsoft.com/dotnet/runtime

# Installer image
FROM amd64/buildpack-deps:noble-curl AS installer

# Retrieve ASP.NET Core
RUN aspnetcore_version=9.0.0 \
    && curl -fSL --output aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/$aspnetcore_version/aspnetcore-runtime-$aspnetcore_version-linux-x64.tar.gz \
    && aspnetcore_sha512='1a81023f119dd5e5b0f9d87b0e3c42df89824b9fcb73192a4670cc2c67358cd018a7c9c965245c7883de468bda88c81d64a21c60f9bc68a6559d76f32d34ce96' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && mkdir -p /dotnet \
    && tar -oxzf aspnetcore.tar.gz -C /dotnet ./shared/Microsoft.AspNetCore.App \
    && rm aspnetcore.tar.gz


# ASP.NET Core image
FROM $REPO:9.0.0-noble-chiseled-extra-amd64

# ASP.NET Core version
ENV ASPNET_VERSION=9.0.0

COPY --from=installer ["/dotnet", "/usr/share/dotnet"]
