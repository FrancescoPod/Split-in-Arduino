# Split-in-Arduino
/* 
 * Author: Francesco Podestà
 * Profession: Student 
 * Contact: francesco.podesta03@gmail.com 
 * Country: Italy
 * 
 * This is an arduino program that 
 * simulates the function split() like java 
 * and it returns an array of strings. 
 * Maybe is not the best way to simulate this very useful function but it works great!
*/

int p = 0;
int o = 0;
void setup() {
 Serial.begin(9600);
 
}




void loop() {
  
  if(Serial.available()){
    String cmd_line = Serial.readString();
    String cmds = cmd_line;
      String chars[cmds.length()];
      
      for(int i = 0; i<cmds.length();i++){
        chars[i] = cmds.charAt(i);   
      }
      String commands[count(chars,cmds.length(),",")+1]; // Delimiter = , you can change it.
      split(chars,",",cmds.length(), cmds, commands); //Call the function. Delimiter = , you can change it.
      // Read output array
      for(int i = 0; i<(sizeof(commands)/sizeof(commands[0]));i++){
        Serial.print("OUT =   ");
        Serial.println(commands[i]);
      }  
  }


}
int count(String args[], int tot, String delim){
  int counter = 0;
  for(int i =0;i<tot;i++){
    if(args[i]==delim){
      counter=counter+1;
    }
    
    
  }
  return counter;
}
int search(String args[], int tot, String delim){

  for(int i = 0; i < tot; i++){
    String str = args[i];
    if(str==delim){
      if(i>p){
        p = i;
        return p;
        
         
      }
    }
    
    
  }
 
}
int older(String args[], int tot, String delim){
  int o;
  for(int k =0;k<tot;k++){
    String indx = args[k];
    if(indx==delim){
      if(k<p){
        o = k;
      }
    }
  }
  return o;
}

void split(String args[], String delim, int tot, String root, String output[]){
  int xt = count(args,tot,delim);
  int old = 0;
   
  for(int j =0; j<xt+1;j++){
    int pos = search(args,tot,delim);
   if(j==0){
     String sub = root.substring(0,pos);
    output[j] = sub;
   }
   else if(j==xt){
    String sub = root.substring(pos+1,root.length());
     output[j] = sub;
   }
   else{
    int ol = older(args,tot,delim);
    String sub = root.substring(ol+1,pos);
     output[j] = sub;
    
   }
   
   
    
  }
  xt = 0;
  p =0;
  
}

