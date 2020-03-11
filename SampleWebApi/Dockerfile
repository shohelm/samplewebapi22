#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.2-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY ["SampleWebApi/SampleWebApi.csproj", "SampleWebApi/"]
RUN dotnet restore "SampleWebApi/SampleWebApi.csproj"
COPY . .
WORKDIR "/src/SampleWebApi"
RUN dotnet build "SampleWebApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SampleWebApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SampleWebApi.dll"]
