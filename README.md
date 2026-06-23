# VPN-hub-and-spoke-punto-a-multipunto-DMVPN-Fase-3-con-IKEv2-con-enrutamiento-din-mico-


**Estudiante:** Juan Francisco Burgos Hiciano  

**Matrícula:** 2023-1981  

**Asignatura:** Seguridad en Redes

📹 Video: https://youtu.be/x0z-dw4opUQ

## Descripción

Implementación de una VPN DMVPN (Dynamic Multipoint VPN) utilizando:

- DMVPN Fase 3
- mGRE (Multipoint GRE)
- NHRP Redirect
- NHRP Shortcut
- IPsec
- IKEv2
- EIGRP

La solución emplea un Hub (IOU3), dos Spokes (IOU2 e IOU4) y un router ISP de tránsito.

## Topología

- IOU3 → Hub DMVPN
- IOU2 → Spoke 1
- IOU4 → Spoke 2
- ISP → Router de tránsito
- PC1 → LAN Site A
- PC2 → LAN Hub
- PC3 → LAN Site B

## 🖼️ Topología

![Topología VPN](https://github.com/jburgoshiciano-source/VPN-hub-and-spoke-punto-a-multipunto-DMVPN-Fase-2-con-IKEv1-con-enrutamiento-din-mico/blob/436cf58052d50526d88901a5d2e7d22d3c1fda1f/DMVPN.png)

## Direccionamiento

| Dispositivo | Dirección |
|------------|-----------|
| Hub Tunnel0 | 172.16.0.1 |
| Spoke1 Tunnel0 | 172.16.0.2 |
| Spoke2 Tunnel0 | 172.16.0.3 |
| LAN Spoke1 | 192.168.1.0/24 |
| LAN Hub | 192.168.100.0/24 |
| LAN Spoke2 | 192.168.2.0/24 |

## Características de DMVPN Fase 3

- Utiliza IKEv2 para negociación de seguridad.
- Implementa:
  - ip nhrp redirect (Hub)
  - ip nhrp shortcut (Spokes)
- Mantiene next-hop-self habilitado.
- Permite sumarización de rutas.
- Escalabilidad superior a DMVPN Fase 2.
- Modelo recomendado por Cisco.

## Seguridad

### IKEv2

- AES-256
- SHA-256
- Grupo DH 14
- Pre-Shared Key

### IPsec

- ESP-AES-256
- ESP-SHA256-HMAC
- Modo Transport

## Verificación

```bash
show dmvpn
show ip nhrp
show crypto ikev2 sa
show crypto ipsec sa
show ip eigrp neighbors
show ip route eigrp
```

## Resultado esperado

Al iniciar comunicación entre PC1 y PC3:

1. El primer paquete atraviesa el Hub.
2. El Hub envía un mensaje NHRP Redirect.
3. El Spoke origen solicita información NHRP.
4. Se crea automáticamente un túnel spoke-to-spoke.
5. El tráfico posterior utiliza la ruta directa.

## Ventajas de DMVPN Fase 3

- Mayor escalabilidad.
- Compatible con sumarización de rutas.
- Menor dependencia del comportamiento del protocolo de enrutamiento.
- Mejor integración con IKEv2.
- Arquitectura recomendada para despliegues empresariales.

## Conclusión

DMVPN Fase 3 mejora significativamente el funcionamiento de DMVPN mediante los mecanismos NHRP Redirect y Shortcut. La combinación de mGRE, NHRP, IPsec e IKEv2 proporciona una solución VPN dinámica, segura y altamente escalable para entornos corporativos modernos.
