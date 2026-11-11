```java

import java.io.Serial;

public class Ergometer {

    private Serial port;
    
    Ergometer(String serialPort) {

        port = new Serial(serialPort, 9600, 8 , 1, 0);

    }
    
    boolean open(){
        return port.open();
    }
    
    boolean reset(){
        
        port.write(CMD_RESET+"\n");

        while(port.dataAvailable <= 0);
        
        return port.readLine().equals(ACK);
        
    }
    
    boolean setPower(int destPower){
        
        port.write(CMD_CHANGEMODE+"\n");
        
        while(port.dataAva);
        
        if (!port.readLine().equals(ACK)) return false;
        
        port.write(CMD_SET_POWER + destPower + "\n");

        while(port.dataAva);

        if (!port.readLine().equals(ACK)) return false;
        
        return true;
    }
    
    String readStatus(){
        
        port.write(CMD_GET_STATUS+"\n");
        
        while(port.dataAvailable() <= 0);
        
        return port.readLine();
    }
    
    void close(){
        
        port.close();
        
    }

}

```