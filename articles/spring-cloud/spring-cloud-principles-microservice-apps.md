---
title: Java und Basisbetriebssystem für Azure Spring Cloud-Microservice-Apps
description: Grundsätze zum Beibehalten der Integrität von Java und Basisbetriebssystem für Azure Spring Cloud-Microservice-Apps
author: MikeDodaro
ms.author: brendm
ms.service: spring-cloud
ms.topic: conceptual
ms.date: 05/27/2020
ms.custom: devx-track-java
ms.openlocfilehash: 1c403398f7320cefa16a4a570645a6d7d750acc7
ms.sourcegitcommit: 58d3b3314df4ba3cabd4d4a6016b22fa5264f05a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/02/2020
ms.locfileid: "89297500"
---
# <a name="java-and-base-os-for-spring-microservice-apps"></a>Java und Basisbetriebssystem für Spring-Microservice-Apps
Im folgenden sind Grundsätze zum Beibehalten der Integrität von Java und Basisbetriebssystem für Spring-Microservice-Apps aufgeführt.
## <a name="principles-for-healthy-java-and-base-os"></a>Grundsätze für die Integrität von Java und Basisbetriebssystem
* Gleiches Basisbetriebssystem für alle Ebenen – Basic | Standard | Premium.
    * Derzeit verwenden Apps in Azure Spring Cloud eine Mischung aus Debian 10 und Ubuntu 18.04.
    * VMware Build Service verwendet Ubuntu 18.04.
* Gleiches Basisbetriebssystem unabhängig von den Startpunkten der Bereitstellung – Quelle | JAR
    * Derzeit verwenden Apps in Azure Spring Cloud eine Mischung aus Debian 10 und Ubuntu 18.04.
* Basisbetriebssystem weist keine Sicherheitsrisiken auf.
    * Das Basisbetriebssystem Debian 10 weist 147 geöffnete CVEs auf.
    * Das Basisbetriebssystem Ubuntu 18.04 weist 132 geöffnete CVEs auf.
* Verwendung von JRE-headless.
    * Derzeit verwenden Apps in Azure Spring Cloud JDK. JRE-headless ist ein kleineres Image.
* Verwendung der neuesten Java-Builds.
    * Derzeit verwenden Apps in Azure Spring Cloud Java 8 Build 242. Dabei handelt es sich um einen veralteten Build.
 
Azul Systems sucht kontinuierlich nach Änderungen an Basisbetriebssystemen und bleibt auf dem Stand der zuletzt erstellten Images. Azure Spring Cloud sucht nach Änderungen an Images und hält Bereitstellungen kontinuierlich auf neuestem Stand.
 
## <a name="faq-for-azure-spring-cloud"></a>Häufig gestellte Fragen zu Azure Spring Cloud

* Welche Versionen von Java werden unterstützt? Hauptversion und Buildnummer.
    * Unterstützung von LTS-Versionen (Java 8 und 11).
    * Verwendung des neuesten Builds, z. B. jetzt Java 8 Build 252 und Java 11 Build 7.
* Wer hat diese Java-Runtimeversionen erstellt?
    * Azul Systems.
* Was ist das Basisbetriebssystem für Images?
    * Ubuntu 20.04 LTS (Focal Fossa). Apps bleiben weiterhin auf der neuesten LTS-Version von Ubuntu.
    * Weitere Informationen finden Sie unter [Ubuntu 20.04 LTS (Focal Fossa)](http://releases.ubuntu.com/focal/).
* Wie kann ich eine unterstützte Java-Runtime für die lokale Entwicklung herunterladen? 
    * Weitere Informationen finden Sie unter [Installieren des JDK für Azure und Azure Stack](https://docs.microsoft.com/azure/developer/java/fundamentals/java-jdk-install).
* Wie erhalte ich Support für Probleme auf der Ebene der Java-Runtime?
    * Öffnen Sie ein Supportticket beim Azure-Support.
 
## <a name="default-deployment-on-azure-spring-cloud"></a>Standardbereitstellung in Azure Spring Cloud

> ![Standardbereitstellung](media/spring-cloud-principles/spring-cloud-default-deployment.png)
 
## <a name="next-steps"></a>Nächste Schritte
* [Schnellstart: Starten einer vorhandenen Azure Spring Cloud-Anwendung über das Azure-Portal](spring-cloud-quickstart.md).
* [Langfristiger Java-Support für Azure und Azure Stack](https://docs.microsoft.com/azure/developer/java/fundamentals/java-jdk-long-term-support)
