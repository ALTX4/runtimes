---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core
{: #dotnet_core}

Die Laufzeit von ASP.NET Core in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'ASP.NET Core'. ASP.NET Core
ist ein modulares Open-Source-Framework zum Erstellen von .NET-Webanwendungen.
.Net Core ist eine kleine, plattformübergreifende Laufzeit, die von ASP.NET Core-Anwendungen als Ziel verwendet werden kann. 
Gemeinsam ermöglichen sie moderne, cloudbasierte Webanwendungen.
{: shortdesc}

## Erkennung
{: #detection}
Das Bluemix-Buildpack 'ASP.NET Core' wird verwendet, wenn mindestens ein Ordner sowohl eine Datei 'project.json' und mindestens eine Datei mit der Erweiterung .cs in der Anwendung enthält wenn die Anwendung mit einer Push-Operation aus dem Ausgabeverzeichnis des Befehls *dotnet publish* übertragen wird.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine ASP.NET Core-Starteranwendung bereit.  Die ASP.NET Core-Starteranwendung ist eine einfache App, die eine Schablone bereitstellt, die Sie verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der Bluemix-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](/docs/cfapps/starter_app_usage.html).

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Übersicht über ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
