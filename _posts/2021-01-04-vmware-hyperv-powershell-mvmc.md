---
date: 2021-01-04T12:00:00.000Z
layout: post
title: Conversão de VM -  VMware para Hyper-v com PowerShell e MVMC
subtitle: ""
description: Embora seja um processo arriscado e traumático, podemos nos ver em
  uma situação que a melhor saída é optar por converter máquinas virtuais de um
  hypervisor a outro.
image: https://res.cloudinary.com/k4bv734/image/upload/v1637712031/blog/vmware-hyperv_lmmzeg.jpg
optimized_image: https://res.cloudinary.com/k4bv734/image/upload/v1637712031/blog/vmware-hyperv-optimized_cabw1p.jpg
category: virtualmachine
tags:
  - virtualmachine
  - vm
  - hyperv
  - vmware
  - hypervisor
  - powershell
  - mvmc
author: brunocosta
paginate: true
---
Embora seja um processo arriscado e traumático, podemos nos ver em uma situação que a melhor saída é optar por converter máquinas virtuais de um hypervisor a outro.  
Neste exemplo de como proceder com essa tarefa, iremos converter uma VM VMware para Hyper-V utilizando o PowerShell e MVMC (Microsoft Virtual Machine Converter).

Primeiro devemos saber qual o disco virtual da máquina virtual do WMware iremos utilizar. O VMware gera vários arquivos ***.vmdk***, se configurado o "split" do HD virtual na criação da VM. Para saber qual utilizará para conversão, entre nas Configurações da VM e na janela das Configurações da Máquina Virtual clique em "Disco rígido". Irá aparecer "Arquivo de disco" e será esse o arquivo a ser considerado. Vou considerar no exemplo o nome ***"vmexemplo-000001.vmdk"***.  

Abra o PowerShell com direitos elevados (administrador) no servidor com a máquina virtual com o VMware.  

No PowerShell, acesse o diretório onde se encontra instalado o VMware. No exemplo irei considerar a pasta de instalação padrão, porém faça conforme sua instalação.  
```
cd "C:\Program Files (x86)\VMware\VMware Workstation"
```

Ainda no Powershell, agora vamos unir os arquivos .vmdk utilizando uma ferramenta do próprio VMware.  
```
vmware-vdiskmanager -r C:\path\vmexemplo-000001.vmdk -t 0 C:\path\vmexemplo-unico.vmdk
```

Substitua o primeiro ***C:\path*** pelo caminho correto onde se encontra o disco da VM VMware e no segundo indique o caminho completo onde deseja salvar o ***.vmdk*** único.  
Mais informações sobre:  
> [https://www.vmware.com/support/ws45/doc/disks_vdiskmanager_eg_ws.html](https://www.vmware.com/support/ws45/doc/disks_vdiskmanager_eg_ws.html)

Agora copie o arquivo gerado para o servidor do Hyper-V (ou deixe reservado em alguma pasta de sua vontade se for o mesmo servidor).  

Próximo passo é instalar o ***MVMC (Microsoft Virtual Machine Converter)***. A Microsoft descontinuou o MVMC e com isso o uso é por conta e risco, além da difícil tarefa de encontrar a ferramenta para download. Pra facilitar nossa vida, segue link para download: 
> [MVMC Download](http://download.microsoft.com/download/9/1/E/91E9F42C-3F1F-4AD9-92B7-8DD65DA3B0C2/mvmc_setup.msi)

Com o MVMC instalado no servidor do Hyper-V, execute o PowerShell como administrador. Execute o comando abaixo para importar um módulo do MVMC:  
```
Import-Module "C:\Program Files\Microsoft Virtual Machine Converter\MvmcCmdlet.psd1"
```

Tudo pronto para, enfim, a conversão. Ainda no PowerShell:  
```
ConvertTo-MvmcVirtualHardDisk "C:\path\vmexemplo-unico.vmdk" -VhdType DynamicHardDisk -VhdFormat Vhdx -DestinationLiteralPath "C:\path\Hyper-V"
```
Lembrando que deve indicar os diretórios desejados em ***"C:\path"***.

Agora é só aguardar a conclusão da conversão, a qual o tempo irá depender do tamanho do seu disco virtual. Após é só criar uma nova VM no Hyper-V indicando o novo disco ***.vhdx*** criado.