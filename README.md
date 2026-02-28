# Taller-Febrero-Linux-2026
Automatización con Ansible para desplegar un entorno NFS completo con servidor, clientes con automontaje y publicación del contenido vía HTTP.

---

## Descripción

Este proyecto implementa un laboratorio reproducible que permite:

- Configurar un servidor NFS y exportar un directorio compartido  
- Configurar clientes Linux con automontaje usando autofs  
- Publicar el contenido del share mediante un servicio systemd con un servidor web en Python  

El objetivo es practicar automatización de infraestructura y configuración de servicios en entornos Linux.

---

## Arquitectura

NFS Server (fileserver)  
└── /srv/nfs/shared (exportado por NFS)

Clientes (grupo ubuntu)  
└── /mnt/shared (montado con autofs)

Servicio adicional  
└── Servidor web Python en puerto 8080 mostrando el contenido del share

---

## Playbooks

| Playbook | Descripción |
|----------|------------|
| `nfs-server.yaml` | Instala y configura el servidor NFS, exporta el directorio y configura firewall |
| `nfs-cliente.yaml` | Configura clientes NFS con automontaje mediante autofs |
| `nfs-systemd.yaml` | Crea y habilita un servicio systemd que publica el share vía HTTP |

---

## Requisitos

- Ansible 2.12 o superior  
- Acceso SSH a los hosts definidos en el inventario  
- Privilegios sudo en los nodos  
- Servidor basado en RHEL / Rocky / AlmaLinux  
- Clientes basados en Ubuntu  

---

## Ejecución

Ejecutar los playbooks en el siguiente orden:

```bash
ansible-playbook -i inventories/hosts.ini playbooks/nfs-server.yaml
ansible-playbook -i inventories/hosts.ini playbooks/nfs-cliente.yaml
ansible-playbook -i inventories/hosts.ini playbooks/nfs-systemd.yaml