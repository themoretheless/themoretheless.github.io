FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY Tmtl.Client.csproj .
RUN dotnet restore Tmtl.Client.csproj
COPY . .
RUN dotnet build Tmtl.Client.csproj -c Release -o /app/build

FROM build AS publish
RUN dotnet publish Tmtl.Client.csproj -c Release -o /app/publish

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot .
COPY nginx.conf /etc/nginx/nginx.conf