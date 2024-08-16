FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /App

# Copy everything
COPY . .
# Restore as distinct layers
RUN ls
# Build and publish a release
RUN dotnet publish -c Release -o out -p:EmulatorMicrosoftPackageVersion=6.0.9

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /App
COPY --from=build-env /App/out .
ENTRYPOINT ["dotnet", "Microsoft.Azure.SignalR.Emulator.dll", "start", "-i", "0.0.0.0"]
