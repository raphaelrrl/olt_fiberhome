# olt_fiberhome
Comandos OLT Fiberhome


HABILITAR INTERFACE UPLINK
Admin\device# set uplink port 19:2 enable
Admin\device# show port 19:2

SETAR INTERFACE MODE DA PORTA UPLINK
Admin\device# set uplink port 9:3 interface_mode sgmii

VERIFICAR TABELA MAC
Admin\fdb# sh fdb slot 19

SETAR GERENCIA OUTBAND
Admin# set debugip 192.168.1.30 mask 255.255.255.0

SETAR GERENCIA INBAND
Admin\service# set manage vlan name GERENCIA vid 4000 inputport 9:3 tagged
Admin\service# set manage vlan name GERENCIA ip 100.127.50.2/30 100.127.50.1

SETAR AUTO SAVE
Admin# sh auto_save
Admin# set auto_save enable period 1440

HABILITAR REDUNDANCIA DAS CONTROLADORAS
Admin# set save sync enable

ENTRAR NO MODO DEBUG
Admin# lll

HABILITAR TODOS OS TRAPS SNMP
Admin(DEBUG_H)> set mib performance switch enable
Admin\device# set mib performance switch enable

HABILITAR ALARMES DA FONTE DE ENERGIA
Admin# set power_alarm enable 1

ALTERAR COMMUNITY SNMP
Admin\service# set snmp community readwrite NOME
Admin\service# set snmp community readonly NOME

FAZER BUSCA DE COMANDOS
Admin# list <string1, string2, stringn>

VERIFICAR TEMPO DE COMPILACAO DO FIRMWARE DA CONTROLADORA
Admin(DEBUG_H)> show debugv

ENTRAR NO MODO DEBUG
Admin# lll

VERIFICAR IP PRIVADO PARA ACESSO AOS CARDS
Admin\service# show privateip

VERIFICA IP PRIVADO PARA ACESSO NAS ONUs
GC8B\service# sh privateip data 0

HABILITAR ACESSO REMOTO A INTERFACE WEB DA ONU PELA WAN
Admin\gpononu# set onu_local_manage_config slot 1 link 16 onu 9 config_enable_switch enable console_switch enable telnet_switch enable web_switch enable web_port 80 web_ani_switch enable tel_ani_switch enable

HABILITAR ACESSO REMOTO A INTERFACE WEB DA ONU PELA WAN GLOBAL
Admin\gpononu# set onu_local_manage_global_config console_switch enable telnet_switch enable web_switch enable web_port 80 web_ani_switch enable tel_ani_switch disable

ADICIONAR COMPATIBILIDADE PARA ONUs DE TELECOM CHINESA
Admin\gponline# set pon_interconnection_switch slot 1 switch enable union_interconnect_switch enable
Admin\gponline# set sys_apply_flag 1

VERIFICAR E REMOVER ALARMES
Admin(DEBUG_H)> sh curalarm
Admin(DEBUG_H)> set end alarm slot 19 pon 2 onu 0 port 0 alarmcode 715

FAZER BACKUP DA OLT
Admin# upload ftp config 192.168.1.32 1 1 OLT.txt
qwr77601357

ATIVAR ONU (PHYSIC_ID) E CONFIGURAR PPPOE
Admin\gpononu# sh discovery slot all link all
Admin\gpononu# sh authorization slot all link all
Admin\gpononu# set authorization slot 2 link 16 type 5506-01-a1 onuid 2 phy_id FHTT06ebe2e0 password null logic_sn fiberhome password fiberhome
Admin\gpononu# set whitelist phy_addr address FHTT06ebe2e0 password null action add
Admin\epononu\qinq# set wancfg sl 2 16 2 ind 1 mode inter ty r 600 0 nat en qos dis qinq dis 33024 65535 1 dsp pppoe pro dis USUARIO SENHA null auto active en
Admin\epononu\qinq# set wanbind sl 2 16 2 ind 1 entr 2 fe1 ssid1

REMOVER QUEBRA DE LINHAS DA CLI
Admin\service# terminal length 0

DEIXAR SESSAO TELNET PERMANENTE
Admin\service# idle-timeout 0

RESTAURAR BACKUP DA OLT
Admin# download ftp config 192.168.1.32 1 1 OLT.txt
Admin# download ftp config <IP_FTP> <USUARIO> <SENHA> <NOME_DO_ARQUIVO.txt>

ATUALIZAR CARD DE CONTROLE
Admin# download ftp system <IP_FTP> <USUARIO> <SENHA> <NOME_DO_ARQUIVO>

ATUALIZAR CARD DE SERVICO
Admin# upgrade xdu <IP_FTP> <USUARIO> <SENHA> <NOME_DO_ARQUIVO> <SLOT>

ALTERAR SENHA DE USUARIO DA CLI
Admin\service# user login-password GEPON
Admin\service# user enable-password GEPON

ADICIONAR USUARIO ADMIN
Admin\service# user add MATHEUS login-password MATHEUS
Admin\service# user role MATHEUS admin enable-password MATHEUS

CONFIGURAR SYSLOG
Admin\service# set syslog_server func enable
Admin\service# set syslog upload level high
Admin\service# set syslog 192.168.1.32 100

LOGS DO CARD GCxB
GC8B\gpon# set io current
GC8B\gpon# set io default

REMOVER BLACKLIST DOS CARDS GCxB
Config\gpon# show onu black-list link 0
Config\gpon# dele onu black-list link 0 sn PDTC-00001122

DESAUTORIZAR CARD
Admin# set card_unauth slot 14

AUTORIZAR CARD
Admin# set card_auth slot 15 type gc8b

VERIFICAR INFORMACOES DO SFP PON
GC8B\gpon# show optical

VERIFICAR SINAL DE ENVIO E RECEPCAO (ONUs) EM UMA PORTA PON
Admin\gponline# sh optic_module_par slot 2 link 1 

DESATIVAR DNS RELAY NA ONU (TELNET ONU)
Config\wan# set wan 0 dnsrelay disable 
Config# save

Remove list ONU
(PON 1/1/|PON 1/2/|PON 1/3/|PON 1/4/|PON 1/5/|PON 1/6/|PON 1/7/|PON 1/8/)
(PON 2/1/|PON 2/2/|PON 2/3/|PON 2/4/|PON 2/5/|PON 2/6/|PON 2/7/|PON 2/8/)
(PON 3/1/|PON 3/2/|PON 3/3/|PON 3/4/|PON 3/5/|PON 3/6/|PON 3/7/|PON 3/8/)
(PON 4/1/|PON 4/2/|PON 4/3/|PON 4/4/|PON 4/5/|PON 4/6/|PON 4/7/|PON 4/8/)
(PON 5/1/|PON 5/2/|PON 5/3/|PON 5/4/|PON 5/5/|PON 5/6/|PON 5/7/|PON 5/8/)
(PON 6/1/|PON 6/2/|PON 6/3/|PON 6/4/|PON 6/5/|PON 6/6/|PON 6/7/|PON 6/8/)
(PON 7/1/|PON 7/2/|PON 7/3/|PON 7/4/|PON 7/5/|PON 7/6/|PON 7/7/|PON 7/8/)
(PON 8/1/|PON 8/2/|PON 8/3/|PON 8/4/|PON 8/5/|PON 8/6/|PON 8/7/|PON 8/8/)
^FE
^SFP
^XFP



Remove not PON ONU
(PON 1/1$|PON 1/2$|PON 1/3$|PON 1/4$|PON 1/5$|PON 1/6$|PON 1/7$|PON 1/8$|PON 1/9$|PON 1/10$|PON 1/11$|PON 1/12$|PON 1/13$|PON 1/14$|PON 1/15$|PON 1/16$)
(PON 2/1$|PON 2/2$|PON 2/3$|PON 2/4$|PON 2/5$|PON 2/6$|PON 2/7$|PON 2/8$)
(PON 3/1$|PON 3/2$|PON 3/3$|PON 3/4$|PON 3/5$|PON 3/6$|PON 3/7$|PON 3/8$)
(PON 4/1$|PON 4/2$|PON 4/3$|PON 4/4$|PON 4/5$|PON 4/6$|PON 4/7$|PON 4/8$)
(PON 5/1$|PON 5/2$|PON 5/3$|PON 5/4$|PON 5/5$|PON 5/6$|PON 5/7$|PON 5/8$)
(PON 6/1$|PON 6/2$|PON 6/3$|PON 6/4$|PON 6/5$|PON 6/6$|PON 6/7$|PON 6/8$)
(PON 7/1$|PON 7/2$|PON 7/3$|PON 7/4$|PON 7/5$|PON 7/6$|PON 7/7$|PON 7/8$)
(PON 8/1$|PON 8/2$|PON 8/3$|PON 8/4$|PON 8/5$|PON 8/6$|PON 8/7$|PON 8/8$)
^SFP
^XFP
^FE




HABILITAR INTERFACE UPLINK
Admin\device# set uplink port 19:2 enable
Admin\device# show port 19:2

SETAR INTERFACE MODE DA PORTA UPLINK
Admin\device# set uplink port 19:2 interface_mode sgmii

VERIFICAR TABELA MAC
Admin\fdb# sh fdb slot 19

SETAR GERENCIA OUTBAND
Admin# set debugip 192.168.1.30 mask 255.255.255.0

SETAR GERENCIA INBAND
Admin\service# set manage vlan name GERENCIA vid 4000 inputport 19:2 tagged
Admin\service# set manage vlan name GERENCIA ip 192.168.1.30/24 192.168.1.1

SETAR AUTO SAVE
Admin# sh auto_save
Admin# set auto_save enable period 1440

HABILITAR REDUNDANCIA DAS CONTROLADORAS
Admin# set save sync enable

ENTRAR NO MODO DEBUG
Admin# lll

HABILITAR TODOS OS TRAPS SNMP
Admin(DEBUG_H)> set mib performance switch enable
Admin\device# set mib performance switch enable

HABILITAR ALARMES DA FONTE DE ENERGIA
Admin# set power_alarm enable 1

ALTERAR COMMUNITY SNMP
Admin\service# set snmp community readwrite NOME
Admin\service# set snmp community readonly NOME

FAZER BUSCA DE COMANDOS
Admin# list <string1, string2, stringn>

VERIFICAR TEMPO DE COMPILACAO DO FIRMWARE DA CONTROLADORA
Admin(DEBUG_H)> show debugv

VERIFICAR IP PRIVADO PARA ACESSO AOS CARDS
Admin\service# show privateip

VERIFICA IP PRIVADO PARA ACESSO NAS ONUs
GC8B\service# sh privateip data 0

HABILITAR ACESSO REMOTO A INTERFACE WEB DA ONU PELA WAN
Admin\gpononu# set onu_local_manage_config slot 1 link 16 onu 9 config_enable_switch enable console_switch enable telnet_switch enable web_switch enable web_port 80 web_ani_switch enable tel_ani_switch enable

HABILITAR ACESSO REMOTO A INTERFACE WEB DA ONU PELA WAN GLOBAL
Admin\gpononu# set onu_local_manage_global_config console_switch enable telnet_switch enable web_switch enable web_port 80 web_ani_switch enable tel_ani_switch disable

ADICIONAR COMPATIBILIDADE PARA ONUs DE TELECOM CHINESA
Admin\gponline# set pon_interconnection_switch slot 1 switch enable union_interconnect_switch enable
Admin\gponline# set sys_apply_flag 0 apply_sence 0

VERIFICAR E REMOVER ALARMES
Admin(DEBUG_H)> sh curalarm
Admin(DEBUG_H)> set end alarm slot 19 pon 2 onu 0 port 0 alarmcode 715

FAZER BACKUP DA OLT
Admin# upload ftp config 192.168.1.32 1 1 OLT.txt

ATIVAR ONU (PHYSIC_ID) E CONFIGURAR PPPOE
Admin\gpononu# sh discovery slot all link all
Admin\gpononu# sh authorization slot all link all
Admin\gpononu# set authorization slot 2 link 16 type 5506-01-a1 onuid 2 phy_id FHTT06ebe2e0 password null logic_sn fiberhome password fiberhome
Admin\gpononu# set whitelist phy_addr address FHTT06ebe2e0 password null action add
Admin\epononu\qinq# set wancfg sl 2 16 2 ind 1 mode inter ty r 600 0 nat en qos dis qinq dis 33024 65535 1 dsp pppoe pro dis USUARIO SENHA null auto active en
Admin\epononu\qinq# set wanbind sl 2 16 2 ind 1 entr 2 fe1 ssid1

DELETAR ONU (PHYSIC_ID)
Admin\gpononu# set whitelist phy_addr address FHTT0901b270 password null action delete slot 2 link 1 onu 1 type 5506-01-a1 

REMOVER QUEBRA DE LINHAS DA CLI
Admin\service# terminal length 0

DEIXAR SESSAO TELNET PERMANENTE
Admin\service# idle-timeout 0

RESTAURAR BACKUP DA OLT
Admin# download ftp config 192.168.1.32 1 1 OLT.txt
Admin# download ftp config <IP_FTP> <USUARIO> <SENHA> <NOME_DO_ARQUIVO.txt>

ATUALIZAR CARD DE CONTROLE
Admin# download ftp system <IP_FTP> <USUARIO> <SENHA> <NOME_DO_ARQUIVO>

ATUALIZAR CARD DE SERVICO
Admin# upgrade xdu <IP_FTP> <USUARIO> <SENHA> <NOME_DO_ARQUIVO> <SLOT>

ALTERAR SENHA DE USUARIO DA CLI
Admin\service# user login-password GEPON
Admin\service# user enable-password GEPON

ADICIONAR USUARIO ADMIN
Admin\service# user add MATHEUS login-password MATHEUS
Admin\service# user role MATHEUS admin enable-password MATHEUS

CONFIGURAR SYSLOG
Admin\service# set syslog_server func enable
Admin\service# set syslog upload level high
Admin\service# set syslog 192.168.1.32 100

LOGS DO CARD GCxB
GC8B\gpon# set io current
GC8B\gpon# set io default

REMOVER BLACKLIST DOS CARDS GCxB
Config\gpon# show onu black-list link 0
Config\gpon# dele onu black-list link 0 sn PDTC-00001122

DESAUTORIZAR CARD
Admin# set card_unauth slot 14

AUTORIZAR CARD
Admin# set card_auth slot 15 type gc8b

VERIFICAR INFORMACOES DO SFP PON
GC8B\gpon# show optical

VERIFICAR SINAL DE ENVIO E RECEPCAO (ONUs) EM UMA PORTA PON
Admin\gponline# sh optic_module_par slot 2 link 1 

DESATIVAR DNS RELAY NA ONU (TELNET ONU)
Config\wan# set wan 0 dnsrelay disable 
Config# save

LAG/LACP
Admin# cd device
Admin\device# set uplink port 19:2 enable 
Admin\device# set uplink port 19:3 enable 
Admin\device# set uplink port 19:2 auto_negotiation disable speed 1000m duplex full
Admin\device# set uplink port 19:3 auto_negotiation disable speed 1000m duplex full
Admin\device# set trunking groupno 1 mode lacp
Admin\device# set trunking groupno 1 criteria sdmac 
Admin\device# set trunking groupno 1 19:2 grouping 19:3 
Admin\device# set slot_separate enable
Admin\device# cd lacp
Admin\device\lacp# set lacp enable 
Admin\device\lacp# set lacp port 19:2 key 1 
Admin\device\lacp# set lacp port 19:3 key 1 
Admin\device# save

EXEMPLO MSTP
Admin\stp# set stp enable
Admin\stp# set stp mode mstp
Admin\stp# set stp region_configuration instance 1 vlan_id 10 to 12
Admin\stp# set stp region_configuration instance 2 vlan_id 20 to 22
Admin\stp# set stp port 9 1 enable
Admin\stp# set stp port 9 2 enable
Admin\stp# set stp instance 1 port 9 2 pathcost 10
Admin\stp# set stp instance 2 port 9 1 pathcost 10

ARQUIVO ONCONFIG (Instalacao do ANM2000)
DBSPACETEMP oltempandbs 
LOGFILES        8
PHYSFILE        200000
ROOTSIZE	512000
