---
title: TCP-UDP
ms.date: 03/30/2017
helpviewer_keywords:
- protocols, TCP/UDP
- network resources, TCP/UDP
- sending data, TCP/UDP
- TCP/UDP
- TcpClient class, about TcpClient class
- application protocols, TCP/UDP
- receiving data, TCP/UDP
- TcpListener class, about TcpListener class
- Socket class, about Socket class
- UDP
- data requests, TCP/UDP
- requesting data from Internet, TCP/UDP
- Internet, TCP/UDP
ms.assetid: df29b4b0-49e8-4923-82b9-13150dfc40f5
ms.openlocfilehash: 261350349497168e3f41b2f6887838d167c3e977
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54692550"
---
# <a name="tcp-udp"></a>TCP-UDP
Las aplicaciones pueden usar servicios de Protocolo de control de transmisión (TCP) y de Protocolo de datagramas de usuario (UDP) con las clases <xref:System.Net.Sockets.TcpClient>, <xref:System.Net.Sockets.TcpListener> y <xref:System.Net.Sockets.UdpClient>. Estas clases de protocolo se basan en la clase <xref:System.Net.Sockets.Socket?displayProperty=nameWithType> y se encargan de los detalles de la transferencia de datos.  
  
 Las clases de protocolo usan los métodos sincrónicos de la clase **Socket** para proporcionar un acceso sencillo y directo a los servicios de red sin la sobrecarga de mantener la información de estado o de conocer los detalles de la configuración de los sockets específicos del protocolo. Para usar métodos **Socket** asincrónicos, puede usar los métodos asincrónicos proporcionados por la clase <xref:System.Net.Sockets.NetworkStream>. Para obtener acceso a las características de la clase **Socket** no expuestas por las clases de protocolo, debe usar la clase **Socket**.  
  
 **TcpClient** y **TcpListener** representan la red mediante la clase **NetworkStream**. Use el método <xref:System.Net.Sockets.TcpClient.GetStream%2A> para devolver la secuencia de red y, luego, llame a los métodos <xref:System.Net.Sockets.NetworkStream.Read%2A> y <xref:System.Net.Sockets.NetworkStream.Write%2A> de la secuencia. La clase **NetworkStream** no posee el socket subyacente de las clases de protocolo, por lo que si la cierra no afectará al socket.  
  
 La clase **UdpClient** usa una matriz de bytes para almacenar el datagrama de UDP. Use el método <xref:System.Net.Sockets.UdpClient.Send%2A> para enviar los datos a la red y el método <xref:System.Net.Sockets.UdpClient.Receive%2A> para recibir un datagrama entrante.  
  
## <a name="see-also"></a>Vea también
- [Uso de servicios TCP](../../../docs/framework/network-programming/using-tcp-services.md)
- [Uso de servicios UDP](../../../docs/framework/network-programming/using-udp-services.md)
- [Uso de secuencias en la red](../../../docs/framework/network-programming/using-streams-on-the-network.md)
- [Uso de un socket de servidor asincrónico](../../../docs/framework/network-programming/using-an-asynchronous-server-socket.md)
- [Uso de un socket de cliente asincrónico](../../../docs/framework/network-programming/using-an-asynchronous-client-socket.md)
- [Usar protocolos de aplicaciones](../../../docs/framework/network-programming/using-application-protocols.md)
