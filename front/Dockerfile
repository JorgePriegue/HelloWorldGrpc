FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY front.csproj .
RUN dotnet restore "front.csproj"
COPY . .
RUN dotnet build "front.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "front.csproj" -c Release -o /app/publish

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot . 
COPY nginx.conf /etc/nginx/nginx.conf