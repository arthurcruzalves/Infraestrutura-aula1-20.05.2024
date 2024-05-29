!Comentários - Desativar comando;
enable

    !Configuração Data e Hora 
    clock set 15:15:00 22 May 2024

    !Modo de Configuração Global
     configure terminal

       !Configuração Hostname
       hostname sw-01

       !Sair de todos os Modos
       end

       service password-encryption

       service timestamps log datetime msec 

       no ip domain-lookup

       banner motd #AVISO: acesso autorizado somente a funcionarios#

       enable secret 123@senac
       
       username senac secret 123@senac
       username arthur password 123@senac
       username admin privilege 15 secret 123@senac

       line console 0

           login local

           password 123@senac

           logging synchronous

           exec-timeout 5 30

    !Salvando da RAM para NVRAM
     copy running-config startup-config 

    !Verificação das Configuração
    show running-config

    enable
    configure terminal 
        !Configuração da VTY
        line vty 0 4
            login local
            password 123@senac 
            logging synchronous
            exec-timeout 5 30
            transport input ssh 
            end 
    write         
--------------------------------------------------------------------------
enable
    configure terminal
        ip default-gateway 192.168.1.254 
        interface vlan 1
            description Interface SVI do SW-01 
            ip address 192.168.1.250 255.255.255.0
            no shutdown 
            end
write 
---------------------------------------------------------
SSH - OpenSSH  
enable
    configure terminal
    ip domain-name senac.br 
    crypto key generate rsa general-keys modulus 1024
    ip ssh version 2
    ip ssh time-out 60
    ip ssh authentication-retries 2
    end
write
