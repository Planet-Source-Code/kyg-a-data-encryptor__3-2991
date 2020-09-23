<div align="center">

## A Data Encryptor


</div>

### Description

A simple encrytor. Password legnth is up to 254, and is not limited to aplphabet, numbers, but also all the characters in the ASCII. Use ALT + 2 or 3 digit number on numpad to key in other characters in ASCII.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[KYG](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/kyg.md)
**Level**          |Beginner
**User Rating**    |4.3 (26 globes from 6 users)
**Compatibility**  |C\+\+ \(general\), Microsoft Visual C\+\+
**Category**       |[Algorithms](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/algorithms__3-29.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/kyg-a-data-encryptor__3-2991/archive/master.zip)





### Source Code

```
#include<fstream.h>
#include<string.h>
void printerror(int);
enum{infileerr,outfileerr,passworderr};
int main(int argc, char* argv[])
  {
  int fileno=1;
  char infilename[255];
  char outfilename[255];
  char password[255];
  char ch;
  cout<<"\t\t\t -----------------------\n";
  cout<<"\t\t\tXilkCipher v1.3\n";
  cout<<"\t\t\t -----------------------\n\n";
  do				//Start for here
    {
    //--------------------------------------
    //   ----------------------------------------
    //
    //Take care of infile
    ++fileno;
    cout<<" Name of file to encrypt/decrypt: ";
    if (argc<2)
      {
      	cin.getline(infilename,255);
    }
    else
      {
      	strcpy(infilename,argv[fileno-1]);
      	cout<<infilename<<"\n";
    }
    ifstream infile(infilename,ios::binary); //prepare infile.
    if (!infile)
      {
      	printerror(infileerr);
      return -1;
    }
    cout<<"\n Name of destination file: ";
    cin.getline(outfilename,255);
    ofstream outfile(outfilename,ios::binary); //prepare outfile.
    if (!outfile)
      {
      	printerror(outfileerr);
      return -1;
    }
    //--------------------------------------
    //   ----------------------------------------
    //
    //Take care of password
    cout<<"\n Password: ";
    for (int i2=0;i2<255;i2++)password[i2]='§';
    cin.getline(password,255);
    int endofstr;
    char passwordcopy[255];
    for (int i1=0;i1<255;i1++)
      {
      	if(password[i1]=='\0')break;
      	endofstr=i1;
    }
    strcpy(passwordcopy,password);
    for (int i=endofstr;i>=0;i--)
      {
      	password[endofstr-i]=password[endofstr-i]&(~passwordcopy[i]);
    }
    //--------------------------------------
    //   ----------------------------------------
    //
    //Encrpyt infile
    int index=0;
    while((infile.read((char*)&ch,sizeof(ch))))
      {
      if (password[index]=='\0') index=0;
      ch=(password[index])^ch; //xor it
      outfile.write((char*)&ch,sizeof(ch));
      index+=1;
    }
    //--------------------------------------
    //   ----------------------------------------
    //
    //Final messages
    infile.close();
    outfile.close();
    cout<<"\n Encryption/Decryption successful.\n\n\n";
  }																/End for here
  while(fileno<argc);
  while ((ch=cin.get())!=ch){cout<<"";}
  return 0;
}
void printerror(int error)
  {
  char ch;
  switch(error)
    {
      	case infileerr:{
      		 cout<<" Error: File not found\n";
      break;
    }
      case outfileerr:{
      cout<<" Error: Unable to create destination file\n";
      break;
    }
      case passworderr:{
      cout<<" Error: Invalid password\n";
      break;
    }
  }
  while ((ch=cin.get())!=ch){cout<<"";}
}
```

