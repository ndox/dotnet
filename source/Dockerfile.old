#   Copyright IBM Corporation 2020
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#        http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

FROM registry.redhat.io/ubi8/dotnet-50 AS buildImg
WORKDIR /src
COPY . .
RUN mkdir app
RUN dotnet restore net5app.csproj
RUN dotnet build net5app.csproj -c Release -o /src/app
RUN dotnet publish net5app.csproj -c Release -o /src/app

# Run Stage
FROM registry.redhat.io/ubi8/dotnet-50 AS runImg
WORKDIR /app
EXPOSE 5000
ENV ASPNETCORE_URLS=http://+:5000
COPY --from=buildImg /src/app .
ENTRYPOINT ["dotnet", "net5app.dll"]
