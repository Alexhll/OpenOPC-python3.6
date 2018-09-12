# OpenOPC-python3.6
OpenOPC for python3.6 enviroment  
This porcedure is for OpenOPC functional test,set your localhost as OPC server.  
MatrikonOPC Server for Simulation is recommended,you can download from [here](https://www.matrikonopc.com/downloads/178/index.aspx).     Make sure these environment variables in your Windows box are set as shown:

 `OPC_CLASS=Matrikon.OPC.Automation;Graybox.OPC.DAWrapper;HSCOPC.Automation;RSI.OPCAutomation;OPC.Automation`
 `OPC_CLIENT=OpenOPC`
 `OPC_GATE_HOST=127.0.0.1`    
 `OPC_GATE_PORT=7766`
 `OPC_HOST=localhost`
 `OPC_MODE=dcom`
 `OPC_SERVER=Hci.TPNServer;HwHsc.OPCServer;opc.deltav.1;AIM.OPC.1;Yokogawa.ExaopcDAEXQ.1;OSI.DA.1;OPC.PHDServerDA.1;Aspen.Infoplus21_DA``.1;National Instruments.OPCLabVIEW;RSLinx OPC Server;KEPware.KEPServerEx.V4;Matrikon.OPC.Simulation;Prosys.OPC.Simulation`

Please download and install the following packages in order to develop your own Python programs.


1. Python 3.6+  
http://www.python.org/download/
 
 
2. Python for Windows Extensions (pywin32)  
You can do pip install through command line by running :`pip install pywin32`
  

3. Pyro4  
You can do pip install through command line by running :`pip install pyro4`
  

4. Clone or download the repository,extract the compressed file to a folder in your windows box (i.e.`C:\OpenOPC36`).


5. Change to lib folder,register the OPC automation wrapper(gbda_aut.dll) by running this in commmand line:  
`C:\OpenOPC36\lib>regsvr32 gbda_aut.dll`
  

6. Change to lib folder,copy python36.dll to your python installation folder if the dll is not existed,folder path as:  
`Lib->site-packages->win32`  
`i.e.` `C:\Users\Administrator\AppData\Local\Programs\Python\Python36\Lib\site-packages\win32`
  

7. Change to src folder,copy OpenOPC.py to your python installation folder,folder path as: `Lib->site-packages`  
`i.e.` `C:\Users\Administrator\AppData\Local\Programs\Python\Python36\Lib\site-packages`
   

8. Install OpenGatewayService  
- Change to src foldre through command line  
`i.e.``C:\OpenOPC36\src>`
  
- Install OpenOPCService through command line  
`python OpenOPCService.py install`

- Wait while the following message is shown  
`Installing service zzzOpenOPCService`  
`Service installed`
    
    
9. Start Open Gateway Service  
net start SERVICE through command line as below:  
`C:\OpenOPC36\bin>net start zzzOpenOPCService`
  
  
10. Functional test  
- using the OpenOPC Gateway Service mode(both win32 platform and non-windows platform)

  client code as below:

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
      
- using DCOM mode(only win32 platform)

     client code as below：

        import OpenOPC
        opc = OpenOPC.client()
        opc.connect("Matrikon.OPC.Simulation.1")
        while True:
            data = opc.read('Random.Int1')[0]
            print(data)

11. The authors of this package are:  
`Copyright (c) 2008-2012 by Barry Barnreiter (barry_b@users.sourceforge.net)`  
`Copyright (c) 2014 by Anton D. Kachalov (mouse@yandex.ru)`  
`Copyright (c) 2017 by José A. Maita (jose.a.maita@gmail.com)`  
For more details please check Mr.joseamaita's repository about OpenOPC [here](https://github.com/joseamaita/openopc120)
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
