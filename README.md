# OpenOPC-python3.6
OpenOPC para ambiente python3.6
Esta porcedure é para o teste funcional OpenOPC, configure seu host local como servidor OPC.
Recomenda-se o MatrikonOPC Server for Simulation, você pode fazer o download a partir de [aqui] (https://www.matrikonopc.com/downloads/178/index.aspx). Verifique se essas variáveis ​​de ambiente na caixa do Windows estão definidas como mostrado:

 `OPC_CLASS=Matrikon.OPC.Automation;Graybox.OPC.DAWrapper;HSCOPC.Automation;RSI.OPCAutomation;OPC.Automation`
 `OPC_CLIENT=OpenOPC`
 `OPC_GATE_HOST=127.0.0.1`    
 `OPC_GATE_PORT=7766`
 `OPC_HOST=localhost`
 `OPC_MODE=dcom`
 `OPC_SERVER=Hci.TPNServer;HwHsc.OPCServer;opc.deltav.1;AIM.OPC.1;Yokogawa.ExaopcDAEXQ.1;OSI.DA.1;OPC.PHDServerDA.1;Aspen.Infoplus21_DA``.1;National Instruments.OPCLabVIEW;RSLinx OPC Server;KEPware.KEPServerEx.V4;Matrikon.OPC.Simulation;Prosys.OPC.Simulation`

Faça o download e instale os seguintes pacotes para desenvolver seus próprios programas Python.

1. Python 3.6+  
http://www.python.org/download/
 
 
2. Python for Windows Extensions (pywin32)  
Você pode instalar o pip através da linha de comando executando :`pip install pywin32`
  

3. Pyro4  
Você pode instalar o pip através da linha de comando executando:`pip install pyro4`
  

Clone ou faça o download do repositório, extraia o arquivo compactado para uma pasta na sua caixa do Windows (i.e.`C:\OpenOPC36`).


5. Mude para a pasta lib, registre o wrapper de automação OPC (gbda_aut.dll) executando isto na linha de comando:
`C:\OpenOPC36\lib>regsvr32 gbda_aut.dll`
  

6. Mude para a pasta lib, copie python36.dll para a pasta de instalação python, se a dll não existir, caminho da pasta como:
`Lib->site-packages->win32`  
`i.e.` `C:\Users\Administrator\AppData\Local\Programs\Python\Python36\Lib\site-packages\win32`
  

7. Mude para a pasta src, copie o OpenOPC.py para a pasta de instalação python, o caminho da pasta como: `Lib->site-packages`  
`i.e.` `C:\Users\Administrator\AppData\Local\Programs\Python\Python36\Lib\site-packages`
   

8. Instale o OpenGatewayService
- Change to src foldre through command line  
`i.e.``C:\OpenOPC36\src>`
  
- Instale o OpenOPCService através da linha de comando
`python OpenOPCService.py install`

- Aguarde enquanto a seguinte mensagem é mostrada
`Installing service zzzOpenOPCService`  
`Service installed`
    
    
9. Iniciar serviço de gateway aberto
net start SERVICE através da linha de comando como abaixo:
`C:\OpenOPC36\bin>net start zzzOpenOPCService`
  
  
10. FTeste funcional
-usando o modo OpenOPC Gateway Service (plataforma win32 e plataforma não-windows)

  código do cliente como abaixo:

      import OpenOPC
       def readopc():
           opchost = 'localhost'
           taglist = ['Random.Int1']
           opc = OpenOPC.open_client(host = opchost)
           opc.connect()
           while True:
               v = opc.read(taglist)
               for i in range(len(v)):
                   (name, val, qual, time) = v[i]
                   print('% -15s % -15s % -15s % -15s'% (name, val, qual, time))
       if __name__=='__main__':
           readopc()
      
- usando o modo DCOM (apenas plataforma win32)

     código do cliente como abaixo:

        import OpenOPC
        opc = OpenOPC.client()
        opc.connect("Matrikon.OPC.Simulation.1")
        while True:
            data = opc.read('Random.Int1')[0]
            print(data)

11. Os autores deste pacote são:
`Copyright (c) 2008-2012 by Barry Barnreiter (barry_b@users.sourceforge.net)`  
`Copyright (c) 2014 by Anton D. Kachalov (mouse@yandex.ru)`  
`Copyright (c) 2017 by José A. Maita (jose.a.maita@gmail.com)`  
For more details please check Mr.joseamaita's repository about OpenOPC [here](https://github.com/joseamaita/openopc120)
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
