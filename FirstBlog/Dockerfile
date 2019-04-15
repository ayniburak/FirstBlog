#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1803 AS base
WORKDIR /app
EXPOSE 54219
EXPOSE 44304

FROM microsoft/dotnet:2.1-sdk-nanoserver-1803 AS build
WORKDIR /src
COPY ["FirstBlog/FirstBlog.csproj", "FirstBlog/"]
RUN dotnet restore "FirstBlog/FirstBlog.csproj"
COPY . .
WORKDIR "/src/FirstBlog"
RUN dotnet build "FirstBlog.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "FirstBlog.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "FirstBlog.dll"]