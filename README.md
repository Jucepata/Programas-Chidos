Libreria uno
================
UNIT JULIO;

 Interface

  Uses Crt,Video,Graph,Dos;

     Procedure Agenda;
     Procedure telmex;
     Procedure factura;
     Procedure Administration;
     Procedure Algebra;

 Implementation

   Var
    horas,minutos,segundos,censeg  :word;
    dia,mes,anio,diasem            :word;


  Procedure Agenda;

   Type
       Registro=Record
       TELEFONO   :String[12];
       NOMBRE     :String[35];
       DOMICILIO  :string[40];
       CEL        :string[15];
       TIPOSAN    :String[2];
       PROFECION  :String[15];
     End;


   Var
     ch           :char;
     Snow         :Salvar;
     Opc          :Char;
     bandera      :boolean;
     ArchivoDatos :File Of Registro;
     RegistroDatos:Registro;
     TotalDatos   :Longint;

     NumeroRegistro :Longint;
     Linea          :Byte;
     Error          :Byte;
   
 PROCEDURE CIRCULO;

   Var
    GraphDriver  :integer;
     GraphMode    :Integer;
     Radius       :Integer;
     OldStyle     :TextSettingsType;

  begin
      GraphDriver := Detect;
  InitGraph(GraphDriver, GraphMode, '\tp6\bgi');
  if GraphResult <> grOk then Halt(1);
  Randomize;

    SetColor(Random(256));
  for Radius := 1 to 80 do
  Begin
    Circle(80,80, Radius*1);
    Circle(80,240, Radius*1);
    Circle(80,400, Radius*1);

    Circle(240,80, Radius*1);
    Circle(240,400, Radius*1);

    Circle(400,80, Radius*1);
    Circle(400,400, Radius*1);

    Circle(560,80, Radius*1);
    Circle(560,240, Radius*1);
    Circle(560,400, Radius*1);
   End;

     SetColor(Random(256));
  for Radius := 1 to 80 do
  Begin
        Circle(240,240, Radius*1);
        Circle(400,240, Radius*1);
   end;

   SetColor(White);
   GetTextSettings(OldStyle);

     SetTextJustify(LeftText, CenterText);

     SetTextStyle(TriplexFont, HorizDir, 5);
     OutTextXY(GetMaxX div 14, GetMaxY div 2,
            'Julio Cesar Pascual Tavarez');

     SetTextStyle(TriplexFont, HorizDir, 5);
     OutTextXY(GetMaxX div 8, GetMaxY div 3,'ESTRUCTURA DE DATOS II');

     SetTextStyle(TriplexFont, HorizDir, 5);

     OutTextXY(GetMaxX div 4, GetMaxY div 5,'SUPER AGENDA');

   with OldStyle do
    begin
      SetTextJustify(Horiz, Vert);
      SetTextStyle(Font, Direction, CharSize);
    end;
     OutTextXY(450,470,'<PULSE CUALQUIER TECLA>');
     ch:=readkey;
   CloseGraph;
end;

  PROCEDURE STILO;

    var
      Gd, Gm   : Integer;
      OldStyle : TextSettingsType;
      Radius   :integer;

   begin
     Gd := Detect; InitGraph(Gd, Gm, '\TP6\BGI');
     if GraphResult <> grOk then Halt(1);

     GetTextSettings(OldStyle);

     SetTextJustify(LeftText, CenterText);

     SetTextStyle(TriplexFont, HorizDir, 5);
     OutTextXY(GetMaxX div 14, GetMaxY div 2,
            'Julio Cesar Pascual Tavarez');

     SetTextStyle(TriplexFont, HorizDir, 5);
     OutTextXY(GetMaxX div 4, GetMaxY div 3,'AGENDA BY');

   with OldStyle do
    begin
      SetTextJustify(Horiz, Vert);
      SetTextStyle(Font, Direction, CharSize);
    end;

     OutTextXY(20,470,'SALIR <PULSE CUALQUIER TECLA>');
  repeat
   delay(50000);
   SetColor(Random(3));
    for Radius := 1 to 80 do
      Begin
       Circle(80,80, Radius*1);
       Circle(550,390, Radius*1);
      end;

    SetColor(Random(3));
     for Radius := 1 to 60 do
      Begin
       Circle(520,60, Radius*1);
      end;
     for Radius := 1 to 40 do
      Begin
       Circle(110,330, Radius*1);
      end;
     until keypressed;
    CloseGraph;
   End;

   Procedure MenuPrincipal;
    Begin
      gotoxy(80,1);
      Panel(1-1,1-1,39,13,red,lightgray,0,False,'','°');
      Panel(1-1,13,39,25+1,lightgreen,lightgray,0,False,'','°');
      Panel(39,13,80+1,25+1,black,lightgray,0,False,'','°');
      Panel(39,1-1,80+1,13,blue,lightgray,0,False,'','°');

      panel(1,1,80,1,Black,lightgray,0,false,'',' ');

      escribe(2,1,4,lightgray,'-');
      escribe(4,1,4,lightgray,'A');
      escribe(5,1,0,lightgray,'ltas');

      escribe(13,1,red,lightgray,'B');
      escribe(14,1,0,lightgray,'ajas');

      escribe(22,1,red,lightgray,'C');
      escribe(23,1,0,lightgray,'onsultas');

      escribe(35,1,red,lightgray,'M');
      escribe(36,1,0,lightgray,'odificaciones');

      escribe(53,1,red,lightgray,'O');
      escribe(54,1,0,lightgray,'bservacion');

      escribe(68,1,red,lightgray,'S');
      escribe(69,1,0,lightgray,'alir');

      panel(1,25,80,25,black,7,0,false,'Programa de Manejo de Archivos',' ');
      escribe(69,25,9,7,'By Tu Padre');

      Panel(10,4,68,22,White,LightGray,2,True,' Agenda ',' ');
      Panel(12,5,66, 8,White,LightGray,1,False,'',' ');
      escribe(28,9,0,lightgray,'* Datos Existentes *');
      Escribe(14,7,red,Blue,'                                                    ');
      Panel(12,10,66,21,White,blue,1,false,'',' ');

      Escribe(14,6,Black,LightGray,'No. Telefono    Nombre');
    End;

    Procedure AbrirArchivo;
     Begin
       Repeat
         Reset(ArchivoDatos);
         Error:=Ioresult;
         If Error=2 Then
           Rewrite(ArchivoDatos)
          Else
           If Error<>0 Then
             MensajeError(Error);
       Until Error=0;
       TotalDatos:=FileSize(ArchivoDatos);
     End;

   Procedure leerDatos(Reg:Longint;Var RegistroDatos:Registro);
    Begin
     Repeat
       Seek(ArchivoDatos,Reg);
       read(ArchivoDatos,RegistroDatos);
       Error:=Ioresult;
       If Error<>0 Then
        MensajeError(Error);
     Until Error=0;
    End;

   Procedure EscribeDatos(Reg:Longint;Var RegistroDatos:Registro);
    Begin
     Repeat
       Seek(ArchivoDatos,Reg);
       write(ArchivoDatos,RegistroDatos);
       Error:=Ioresult;
       If Error<>0 Then
        MensajeError(Error);
     Until Error=0;
    End;


   Procedure EscribePantalla(Reg:Longint;RegistroDatos:Registro;Linea:Byte;Resaltado:Boolean);
     Var
      Cad  :String[10];

    Begin
     Str(Reg:3,Cad);
     With RegistroDatos Do
      Begin
       If Resaltado Then
          Begin
            Escribe(14,7,red,Blue,'                                                    ');
            Escribe(13,7,lightred,Blue,Cad);
            Escribe(18,7,yellow,Blue,TELEFONO);
            Escribe(30,7,yellow,Blue,Nombre);

            Escribe(14,10+Linea,lightgreen,Blue,Cad);
            Escribe(14,10+Linea,lightred,Blue,'¯');
            Escribe(65,10+Linea,White,Blue,'Û');                                                        {©°Ûþ}
            Escribe(18,10+Linea,lightgreen,Blue,Telefono);
            Escribe(28,10+Linea,lightgreen,Blue,Nombre);
          End
        Else
          Begin
            Escribe(14,10+Linea,white,blue,Cad);
            Escribe(14,10+Linea,lightgreen,Blue,' ');
            Escribe(65,10+Linea,lightblue,Blue,'Û');
            Escribe(18,10+Linea,white,blue,Telefono);
            Escribe(28,10+Linea,white,blue,Nombre);
          End
      End;
   end;


   Procedure MostrarDatos(Reg:Longint);

     Var
      I    :Byte;
      Linea:Byte;

    Begin
      Linea:=1;
      Panel(12,10,66,21,White,blue,1,False,'',' ');
      For I:=Reg To (Reg+9) Do
       If I<TotalDatos Then
        Begin
          LeerDatos(I,RegistroDatos);
          EscribePantalla(I,RegistroDatos,Linea,False);
          Linea:=Linea+1;
        End;
    End;

   PROCEDURE BORRAR(Numeroregistro:longint);

     VAR
     i,totalTmp  :longint;
     ArcTmp      :file of registro;

      begin
        Assign(arctmp,'AGENDA.tmp');
        rewrite(arctmp);
        totaltmp :=0;

        for i:=0 to (totaldatos-1) do
        begin
          if i<> numeroregistro then
          begin
            leerdatos(i,registrodatos);
            seek(ArcTmp,totaltmp);
            write(arctmp,registrodatos);
            totaltmp := filesize(arctmp);
          end;
        end;

           close(arctmp);
           close(archivodatos);
           erase (archivodatos);
           rename(arctmp,'AGENDA.dat');
           abrirarchivo;
      end;


   Procedure Altas;
      Var
       Lonche:Salvar;
       Opc   :Char;

    Begin
      SalvarPantalla(Lonche);
      Repeat
      with RegistroDatos do
       begin
       Textbackground(blue);
          Gotoxy(80,1);

          Panel(14,3,65,8,White,LightGray,2,True,' ALTAS ',' ');
          Panel(20,4,63,7,White,BLUE,0,FALSE,'',' ');

          Escribe(15,4,Black,LightGray,'NOMBRE:');
          Escribe(15,5,black,LightGray,'DOMICILIO:');
          Escribe(15,6,black,LightGray,'TELEFONO: ');
          Escribe(35,6,black,LightGray,' CEL:');
          Escribe(15,7,black,LightGray,'TIPO SANG:');
          Escribe(35,7,black,LightGray,' PROFECION:');
         Textcolor(yellow);
          gotoxy(23,4);readln(nombre);
          gotoxy(26,5);readln(DOMICILIO);
          gotoxy(26,6);readln(TELEFONO);
          gotoxy(41,6);readln(CEL);
          gotoxy(26,7);readln(TIPOSAN);
          gotoxy(47,7);readln(PROFECION);
          {Escribe(42,8,black,LightGray,'gr. Observacion [s/n] ');
          escribe(40,8,red,LightGray,' A');}
       end;

         Panel(20,15,52,17,white,Lightgray,1,true,'',' ');
         Escribe(22,16,white,blue,'LOS DATOS SON CORRECTOS [S/N]');

         Opc:=Upcase(Readkey);
       Until Opc='S';

       EscribeDatos(totaldatos,registrodatos);
       TotalDatos:=FileSize(Archivodatos);

      RestaurarPantalla(Lonche);
    End;

    Procedure Bajas;
      Var
       Lonche:Salvar;
       Opc   :Char;
    Begin
      SalvarPantalla(Lonche);
       Panel(14,13,65,18,White,LightGray,2,True,' BAJAS ',' ');
          Panel(20,14,63,17,White,BLUE,0,FALSE,'',' ');

          Escribe(15,14,Black,LightGray,'NOMBRE:');
          Escribe(15,15,black,LightGray,'DOMICILIO:');
          Escribe(15,16,black,LightGray,'TELEFONO: ');
          Escribe(35,16,black,LightGray,' CEL:');
          Escribe(15,17,black,LightGray,'TIPO SANG:');
          Escribe(35,17,black,LightGray,' PROFECION:');

        With RegistroDatos Do
         Begin

          Escribe(23,14,yellow,blue,nombre);
          Escribe(26,15,yellow,blue,DOMICILIO);
          Escribe(26,16,yellow,blue,TELEFONO);
          Escribe(41,16,yellow,blue,CEL);
          Escribe(26,17,yellow,blue,TIPOSAN);
          Escribe(47,17,yellow,blue,PROFECION);
        End;

       Escribe(27,18,red+Blink,LightGray,' BORRAR EL REGISTRO [S/N] ');

       Repeat
         Opc:=Upcase(Readkey);
       Until Opc in ['S','N'];

        IF opc= 'S' then
           borrar(numeroregistro);

      RestaurarPantalla(Lonche);
    End;

   Procedure Consultas;
      Var
       Lonche:Salvar;
       Opc   :Char;
    Begin
      SalvarPantalla(Lonche);
          Gotoxy(80,1);

          Panel(14,13,65,18,White,LightGray,2,True,' CONSULTAS ',' ');
          Panel(20,14,63,17,White,BLUE,0,FALSE,'',' ');

          Escribe(15,14,Black,LightGray,'NOMBRE:');
          Escribe(15,15,black,LightGray,'DOMICILIO:');
          Escribe(15,16,black,LightGray,'TELEFONO: ');
          Escribe(35,16,black,LightGray,' CEL:');
          Escribe(15,17,black,LightGray,'TIPO SANG:');
          Escribe(35,17,black,LightGray,' PROFECION:');
     
        With RegistroDatos Do
         Begin

          Escribe(23,14,yellow,blue,nombre);
          Escribe(26,15,yellow,blue,DOMICILIO);
          Escribe(26,16,yellow,blue,TELEFONO);
          Escribe(41,16,yellow,blue,CEL);
          Escribe(26,17,yellow,blue,TIPOSAN);
          Escribe(47,17,yellow,blue,PROFECION);
        End;

        Escribe(18,18,black,LightGray,' Pulse <   > Para Salir ');
        Escribe(26,18,red+Blink,LightGray,'Esc');
        Escribe(50,18,black,LightGray,'bservaciones ');
        Escribe(48,18,Red,LightGRAY,' O');

    opc:=upcase(readkey);
    
     if opc = 'O' then
     
      begin
             Panel(19,20,65,24,White,LightGray,2,True,' OBSERVACIONES ',' ');
             Panel(20,21,63,23,White,BLUE,0,FALSE,'',' ');
             Escribe(30,24,red,LightGray,' Pulse <   > Para Salir ');
             Escribe(38,24,red+Blink,LightGray,'Esc');

          Repeat
           Opc:=Readkey;
          Until Opc=#27;
         end;

      RestaurarPantalla(Lonche);
    End;

   Procedure Modificaciones;
      Var
       Lonche:Salvar;
       Opc   :Char;
    Begin
      SalvarPantalla(Lonche);

     with RegistroDatos do
       begin
       Textbackground(blue);
       Panel(14,3,65,8,White,LightGray,2,True,' MODIFICACIONES ',' ');
          Panel(20,4,63,7,White,BLUE,0,FALSE,'',' ');

          Escribe(15,4,Black,LightGray,'NOMBRE:');
          Escribe(15,5,black,LightGray,'DOMICILIO:');
          Escribe(15,6,black,LightGray,'TELEFONO: ');
          Escribe(35,6,black,LightGray,' CEL:');
          Escribe(15,7,black,LightGray,'TIPO SANG:');
          Escribe(35,7,black,LightGray,' PROFECION:');
         end;

         With RegistroDatos Do
          Begin

             Escribe(23,4,yellow,blue,nombre);
             Escribe(26,5,yellow,blue,DOMICILIO);
             Escribe(26,6,yellow,blue,TELEFONO);
             Escribe(41,6,yellow,blue,CEL);
             Escribe(26,7,yellow,blue,TIPOSAN);
             Escribe(47,7,yellow,blue,PROFECION);
          End;

       Panel(20,15,47,17,white,lightgray,1,true,'',' ');
       Escribe(22,16,white,blue,'MODIFICAR LOS DATOS [S/N]');

      Repeat
        Opc:=Upcase(Readkey);
      Until opc in ['S','N'];

    IF OPC = 'S' Then
     Begin
      Repeat

      with RegistroDatos do
       begin
         Textbackground(blue);

         Panel(14,3,65,8,White,LightGray,2,True,' MODIFICACIONES ',' ');
          Panel(20,4,63,7,White,BLUE,0,FALSE,'',' ');

          Escribe(15,4,Black,LightGray,'NOMBRE:');
          Escribe(15,5,black,LightGray,'DOMICILIO:');
          Escribe(15,6,black,LightGray,'TELEFONO: ');
          Escribe(35,6,black,LightGray,' CEL:');
          Escribe(15,7,black,LightGray,'TIPO SANG:');
          Escribe(35,7,black,LightGray,' PROFECION:');
         Textcolor(yellow);
          gotoxy(23,4);readln(nombre);
          gotoxy(26,5);readln(DOMICILIO);
          gotoxy(26,6);readln(TELEFONO);
          gotoxy(41,6);readln(CEL);
          gotoxy(26,7);readln(TIPOSAN);
          gotoxy(47,7);readln(PROFECION);
       end;

         Panel(20,15,52,17,white,lightgray,1,true,'',' ');
         Escribe(22,16,white+Blink,blue,'LOS DATOS SON CORRECTOS [S/N]');

         Opc:=Upcase(Readkey);
       Until Opc='S';

       EscribeDatos(NumeroRegistro,registrodatos);
      end;
      RestaurarPantalla(Lonche);
    End;

   Procedure DecideOpcion(Opc:Char);
    Begin
    
       Case Opc Of
         
         'a','A': Begin
                     ALTAS;
                     MostrarDatos(NumeroRegistro-linea+1);
                   end;

         'b','B':  if totaldatos>0 then
               begin
                 BAJAS;
                  if numeroregistro=totaldatos then
                   begin
                     numeroregistro:=numeroregistro-1;
                      if linea>1 then
                     linea:=linea-1;
                   end;
                  MostrarDatos(NumeroRegistro-linea+1);
               end;

         'c','C':Begin
                  If TotalDatos>0 Then
                    Consultas;
                End;

         'm','M': if not (bandera) then
                 Begin
                   Modificaciones;
                   MostrarDatos(NumeroRegistro-Linea+1);
                 end;


            #72:Begin
              if bandera then
                 If (TotalDatos>0) And (NumeroRegistro>0) Then
                   Begin
                     EscribePantalla(NumeroRegistro,RegistroDatos,Linea,False);

                     If Linea>1 Then
                        Linea:=Linea-1
                      Else
                        MostrarDatos(NumeroRegistro-Linea);

                     NumeroRegistro:=NumeroRegistro-1;
                   End;
                End;
            #80:Begin
              if bandera then
                 If (TotalDatos>0) And (NumeroRegistro<TotalDatos-1) Then
                   Begin
                     EscribePantalla(NumeroRegistro,RegistroDatos,Linea,False);

                     If Linea<10 Then
                        Linea:=Linea+1
                      Else
                        MostrarDatos(NumeroRegistro-Linea+2);

                     NumeroRegistro:=NumeroRegistro+1;
                   End;
                End;
       End;
    End;

   Label Salir,Salir2;

   Begin
   Gotoxy(80,1);
     SalvarPantalla(Snow);

     Assign(ArchivoDatos,'AGENDA.DAT');
     AbrirArchivo;
     If Error<>0 Then
       Goto Salir;

      Circulo;
      MenuPrincipal;

      Linea:=1;
      NumeroRegistro:=0;

      If TotalDatos>0 Then
        MostrarDatos(NumeroRegistro);


      Repeat
          bandera:=false;

          If TotalDatos>0 Then
           Begin
             LeerDatos(NumeroRegistro,RegistroDatos);
             EscribePantalla(NumeroRegistro,RegistroDatos,Linea,True);
           End;

          Opc:=upcase(Readkey);

           if opc = #0 then
            begin
              Opc:=upcase(Readkey);
              bandera:=true;
            end;

           if opc in ['S',#27] then
            begin
              STILO;
            end;

          DecideOpcion (Opc);

      Until Opc in ['S',#27];

     Salir2: ;

     Close(ArchivoDatos);

     Salir: ;

     RestaurarPantalla(Snow);
    end;



  Procedure telmex;

    Var
      renta,rm,llre,minllnac,minllint :real;
      minllpc, m1,m2,m3,m4,m5,total   :real;
      tllloc,tllnac,tllint,tc,tcllp   :real;
      ic1,ic2,ic3,ic4,ic5,llpp,celu   :real;
      sllloc :real;
      sllnac :real;
      sllint :real;
      sllc   :real;
      sllcllp:real;
      tlllco :real;
      timp,tmin :real;
      imptotal,iva,subt :real;
      Descuento1 :real;
      Descuento2 :real;
      Descuento3 :real;
      Descuento4 :real;
      opc                        :char;

   Const
       x=5;
       y=1;

Begin
   textbackground(white);
   clrscr;
   textcolor(blue);

       gotoxy(x+13,y);   write('ÜÜÜÜÜ ÜÜÜÜÜ Ü     ÜÜ   ÜÜ ÜÜÜÜÜ  Ü     Ü');
       gotoxy(x+13,y+1); write('  Û   Û     Û     Û ßÜß Û Û       ßÜ Üß ');
       gotoxy(x+13,y+2); write('  Û   Ûßßßß Û     Û     Û Ûßßßß    ÜßÜ  ');
       gotoxy(x+13,y+3); write('  Û   ÛÜÜÜÜ ÛÜÜÜÜ Û     Û ÛÜÜÜÜ  Üß   ßÜ © ');
       textcolor(RED);
       gotoxy(x+17,y+5); write('TELEFONOS DE MEXICO S.A.B. de C.V.');
       textcolor(black);
        gotoxy(x,y+7);  write('ESTE RECIBO CUENTA CON RENTA, LLAMADAS REALIZADAS, ');
        gotoxy(x,y+8);  write('LLAMADA A CELULAR,TARIFA Y LLAMADAS POR PAGAR QUE USTED');
        gotoxy(x,y+9);  write('TENDRA QUE LLENAR PARA DESPUES MOSTRARLE SU RECIBO. ');

        gotoxy(x,y+11);  write('*RENTA:');
        gotoxy(x,y+12);  write('*LLAMADAS DE RENTA MENSUAL:');
        gotoxy(x,y+13);  write('*LLAMADAS LOCALES REALIZADAS:');
        gotoxy(x,y+14);  write('*MINUTOS DE LLAMADAS NACIONALES:');
        gotoxy(x,y+15);  write('*MINUTOS DE LLAMADAS INTERNACIONALES:');
        gotoxy(x,y+16);  write('*MINUTOS DE LLAM. A CEL."EL QUE LLAMA PAGA":');
        gotoxy(x,y+17);  write('*MINUTOS DE 5 LLAMADAS A CELULARES:   ³   ³   ³   ³   ³   ³ ');

        textcolor(blue);

        gotoxy(x+8,y+11);  readln(renta);
        gotoxy(x+29,y+12); readln(rm);
        gotoxy(x+30,y+13); readln(llre);
        gotoxy(x+33,y+14); readln(minllnac);
        gotoxy(x+37,y+15); readln(minllint);
        gotoxy(x+46,y+16); readln(minllpc);

        gotoxy(x+40,y+17); readln(m1);
        gotoxy(x+44,y+17); readln(m2);
        gotoxy(x+48,y+17); readln(m3);
        gotoxy(x+52,y+17); readln(m4);
        gotoxy(x+56,y+17); readln(m5);

        tllloc:=1.15;
        tllnac:=2.30;
        tllint:=5.64;
        tc    :=3.65;
        tcllp :=1.72;

        ic1:=m1*tc;
        ic2:=m2*tc;
        ic3:=m3*tc;
        ic4:=m4*tc;
        ic5:=m5*tc;

        llpp   :=llre-rm;
        tmin   :=m1+m2+m3+m4+m5;
        sllloc :=tllloc*llpp;
        sllnac :=tllnac*minllnac;
        sllint :=tllint*minllint;
        sllc   :=ic1+ic2+ic3+ic4+ic5;
        sllcllp:=tcllp*minllpc;
        Celu   :=sllc+sllcllp;           

        imptotal:=sllloc+sllnac+sllint+celu+renta;
        iva :=0.16*imptotal;
        subt :=imptotal+iva;


        begin
          Descuento1 := 0.10 * subt;
          Descuento2 := 0.20 * subt;
          Descuento3 := 0.25 * subt;
          Descuento4 := 0.35 * subt;

       clrscr;
       textcolor(blue);

             if (subt < 499) or (subt =500) then
              begin
                Total:=subt-descuento1;
                gotoxy(x+67,y+20); write(descuento1:5:2);
              end;

             if (subt >501) and (subt< 799) then
              begin
                Total:=subt-descuento2;
                gotoxy(x+67,y+20); write(descuento2:5:2);
              end;


             if (subt > 800) and (subt < 999) then
              begin
                Total:=subt-descuento3;
                gotoxy(x+67,y+20); write(descuento3:5:2);
              end;

             if subt >1000 then
              begin
                Total:=subt-descuento4;
                gotoxy(x+67,y+20); write(descuento4:5:2);
              end;

       gotoxy(x+13,y);   write('ÜÜÜÜÜ ÜÜÜÜÜ Ü     ÜÜ   ÜÜ ÜÜÜÜÜ  Ü     Ü');
       gotoxy(x+13,y+1); write('  Û   Û     Û     Û ßÜß Û Û       ßÜ Üß ');
       gotoxy(x+13,y+2); write('  Û   Ûßßßß Û     Û     Û Ûßßßß    ÜßÜ  ');
       gotoxy(x+13,y+3); write('  Û   ÛÜÜÜÜ ÛÜÜÜÜ Û     Û ÛÜÜÜÜ  Üß   ßÜ © ');
       textcolor(RED);
       gotoxy(x+17,y+5); write('TELEFONOS DE MEXICO S.A.B. de C.V.');
       textcolor(black);

      gotoxy(x,y+7);  write('GARCILASO DE LA VEGA');
      gotoxy(x,y+8);  write('Calle Palmera 2563');
      gotoxy(x,y+9);  write('francisco');
      gotoxy(x,y+10); write('Polanquito');
      gotoxy(x,y+11); write('C.P.44969-CR-44943');

      gotoxy(x+40,y+7);  write('TOTAL A PAGAR: ');
      gotoxy(x+40,y+8);  write('PAGAR ANTES DE:  15-ENERO-2012');
      gotoxy(x+40,y+9);  write('MES DE FACTURACION:  diciembre');
      gotoxy(x+40,y+10); write('TELEFONO:        (33) 36460245');
      gotoxy(x+40,y+11); write('FACTURA:       120308090038147');
      textcolor(RED);
      gotoxy(x+60,y+7);  write(total:5:2);

      gotoxy(x,y+13);  write('ESTADO DE CUENTA________________________________________________________');
      gotoxy(x,y+16); write('Saldo                                                               0.00 ');

      textcolor(BLACK);
      gotoxy(x,y+14);  write('Saldo anterior                                                  $ 194.00 ');
      gotoxy(x,y+15);  write('Su pago   (Gracias)                                              -194.00 ');

      gotoxy(x,y+17); write('Cargo del mes                                                     ',imptotal:5:2);
      gotoxy(x,y+18); write('IVA                                                               ',iva:5:2);
      gotoxy(x,y+19); write('Sub Total                                                         ',subt:5:2);
      gotoxy(x,y+20); write('Descuento');
      gotoxy(x,y+21); write('Total a Pagar');
      gotoxy(x+13,y+21); write('___________________________________________________________');

      gotoxy(x+64,y+17); write(imptotal:8:2);
      gotoxy(x+64,y+18); write(iva:8:2);
      gotoxy(x+64,y+19); write(subt:8:2);
      textcolor(RED);
      gotoxy(x+64,y+21);  write(total:8:2);
    readln;

      gotoxy(x,y+23); writeln('CARGOS DEL MES ');
      textcolor(black);
      writeln('    Cargo del mes                                      ',imptotal:5:2);
      writeln('    Celulares                                          ',celu:5:2);
      writeln('    Sub Total                                          ',subt:5:2);
      writeln('    GARSILASO DE LA VEGA');
      writeln('    Telefono: (33)36460245            Total a Pagar: $ ',total:5:2);
      writeln('    Mes de facturacion: Diciembre     Pagar antes de: 15-enero-2012 ');
      writeln('    ------------------------------------------------------------------------');
    readln;

      textcolor(RED);
      writeln('    SERVICIO LOCAL');
      textcolor(black);
      writeln('    Descripcion                                                     importe');
      writeln('    RENTA                                                           ',rm:5:2);
      writeln('                                                TOTAL               ',rm:5:2);
      writeln('    ------------------------------------------------------------------------');
      writeln('    Llamadas                                   cantidad           periodo');
      writeln('    Llamadas realizadas                         ',llre:5:2,'           enero 2010');
      writeln('    Llamadas incluidas en la renta mensual      ',rm:5:2);
      writeln('    Llamadas por pagar                          ',llpp:5:2);
      writeln('    tarifa                                      ',tllloc:5:2);
      writeln('    Total                                       ',sllloc:5:2);
      writeln('    ------------------------------------------------------------------------');
     readln;

      textcolor(RED);
      writeln('    CELULARES');
      textcolor(black);
      writeln('    Descripcion                                                     importe   ');
      writeln('    Llamadas a celular "EL QUE LLAMA PAGA" 044');
      writeln('                                                TOTAL               ',sllcllp:5:2);
      writeln('    ------------------------------------------------------------------------');
      writeln;
      writeln;
      textcolor(RED);
      writeln('    fecha        hora       telefono        minutos     importe');
      textcolor(black);
      writeln('    ------------------------------------------------------------------------');
      writeln('    Dic-09   ³   19:00  ³   1125 6489   ³     ',m1:5:2,' ³  ',ic1:5:2 );
      writeln('    Dic-13   ³   21:05  ³   1254 7836   ³     ',m2:5:2,' ³  ',ic2:5:2 );
      writeln('    Dic-24   ³   18:30  ³   3265 8974   ³     ',m3:5:2,' ³  ',ic3:5:2 );
      writeln('    Dic-24   ³   14:50  ³   3865 9741   ³     ',m4:5:2,' ³  ',ic4:5:2 );
      writeln('    Dic-25   ³   11:10  ³   3605 4121   ³     ',m5:5:2,' ³  ',ic5:5:2 );
      writeln('    ------------------------------------------------------------------------');
      writeln('                              Total           ',tmin:5:2,'    ',sllc:5:2 );
      writeln;
      writeln('   *Total con letra: ');
      textcolor(blue);
      
       opc:=readkey;
      end;
    end;


    function segundo:string;
      begin
          segundos:=00;
            repeat
             for segundos:= 0 to 60 do
                begin
                 segundos:=segundos+1;
                 write(segundos:2);
        end;
    until segundos =60;
  end;


  Procedure factura;

  Var
    C1,C2,C3,C4,C5   :real;
    m1,m2,m3,m4,m5   :real;
    Depto  :string[20];
    Nombre :string[50];
    tel    :string[15];
    fecent :string[20];
    DESC   :string;
    PU     :real;
    MONTO  :byte;
    TOTAL  :real;
    SUBT   :real;
    IVA    :real;
    I      :byte;
    OPC    :char;


  
  Const
    X=6;
    Y=13;


   function meses:string;
   begin
      case mes of
        1:meses :='01';
        2:meses :='02';
        3:meses :='03';
        4:meses :='04';
        5:meses :='05';
        6:meses :='06';
        7:meses :='07';
        8:meses :='08';
        9:meses :='09';
       10:meses :='10';
       11:meses :='11';
       12:meses :='12';
     end;
  end;


  begin
   textbackground(white);
    clrscr;

     getdate(anio,mes,dia,diasem);

     Panel(1,1,80,25,black,lightgray,2,false,'',' ');
     Escribe(3,25,black,LIGHTGRAY,' Julio Cesar Pascual Tavarez ');
     textcolor(black);

      gotoxy(x+10,y-11); write('U N I V E R S I D A D  D E  G U A D A L A J A R A');
      gotoxy(x+16,y-10); write('');
      gotoxy(x+20,y-9); write('CUCEI');
      gotoxy(x+6,y-7); write('REVOLUCION 1450 COLONIA TLAQUEPAQUE, JALISCO, MEXICO');
      gotoxy(x+20,y-6); write('Tels. 36565753 y fax 36330613');
      gotoxy(x+24,y-5); write('R.F.C UDG-081519-CM2');

        textcolor(red);
        gotoxy(x+64,y-4); write('36196');
        gotoxy(X+60,Y-3); write(dia,'/',meses,'/', anio);
        textcolor(black);
        gotoxy(x+49,y-4); write('Nota de Venta:');
        gotoxy(x+1,y-3); write('Departamento:');
        gotoxy(x+25,y-1); write('Entrega:');
        gotoxy(x+52,y-3); write('Fecha:');
        gotoxy(x+52,y-2); write('Hora:');
        gotoxy(x+52,y-1); write('Folio: C-9785');
        gotoxy(x+1,y-2); write('Nombre:');
        gotoxy(x+1,y-1); write('Telefono:');

      textcolor(black);
      gotoxy(x,y);    write('Ú-----------Â---------------Â-------------------Â-------------------¿');
      gotoxy(x,y+1);  write('³           ³               ³                   ³                   ³');
      gotoxy(x,y+2);  write('³           ³               ³                   ³                   ³');
      gotoxy(x,y+3);  write('³           ³               ³                   ³                   ³');
      gotoxy(x,y+4);  write('³           ³               ³                   ³                   ³');
      gotoxy(x,y+5);  write('³           ³               ³                   ³                   ³');
      gotoxy(x,y+6);  write('³           ³               ³                   ³                   ³');
      gotoxy(x,y+7);  write('³___________³_______________³___________________³___________________³');
      gotoxy(x,y+8);  write('                                                ³                   ³');
      gotoxy(x,y+9);  write('                                                ³                   ³');
      gotoxy(x,y+10); write('                                                ³___________________³');

       textcolor(black);

      gotoxy(x+2,y+1);   write('CANTIDAD');
      gotoxy(x+14,y+1);   write('DESCRIPCION');
      gotoxy(x+30,y+1);  write('PRECIO UNITARIO');
      gotoxy(x+50,y+1);  write('MONTO TOTAL');

      gotoxy(x+49,y+8); write('SUBTOTAL');
      gotoxy(x+49,y+9); write('IVA');
      gotoxy(x+49,y+10); write('TOTAL');

      textcolor(DarkGray);
        gotoxy(x+15,y-3); Readln(depto);
        gotoxy(x+9,y-2);  Readln(nombre);
        gotoxy(x+11,y-1); Readln(tel);
        gotoxy(x+34,y-1); Readln(fecent);

      textcolor(white);

         begin


            Gotoxy(x+5,y+2);  readln(C1);
            Gotoxy(x+15,y+2); readln(DESC);
            Gotoxy(x+36,y+2); readln(PU);

               begin
                m1 :=c1*pu;
                gotoxy(x+55,y+2); write(m1:5:2);
               end;

            Gotoxy(x+5,y+3);  readln(C2);
            Gotoxy(x+15,y+3); readln(DESC);
            Gotoxy(x+36,y+3); readln(PU);

             begin
                m2 :=c2*pu;
                gotoxy(x+55,y+3); write(m2:5:2);
               end;

            Gotoxy(x+5,y+4);  readln(C3);
            Gotoxy(x+15,y+4); readln(DESC);
            Gotoxy(x+36,y+4); readln(PU);

             begin
                m3 :=c3*pu;
                gotoxy(x+55,y+4); write(m3:5:2);
               end;

            Gotoxy(x+5,y+5);  readln(C4);
            Gotoxy(x+15,y+5); readln(DESC);
            Gotoxy(x+36,y+5); readln(PU);

              begin
                m4 :=c4*pu;
                gotoxy(x+55,y+5); write(m4:5:2);
               end;

            Gotoxy(x+5,y+6);  readln(C5);
            Gotoxy(x+15,y+6); readln(DESC);
            Gotoxy(x+36,y+6); readln(PU);

             begin
                m5 := c5*pu;
                gotoxy(x+55,y+6); write(m5:5:2);
              end;

             begin
                subt := m1+m2+m3+m4+m5;
                gotoxy(x+53,y+8); write(subt:8:2);

                iva := subt * 0.15;
                gotoxy(x+53,y+9); write(iva:8:2);

                total := subt+iva;
                textcolor(red);
                gotoxy(x+54,y+10); write(total:8:2);
                  begin
                   gettime(horas,minutos,segundos,censeg);
                    repeat
                     gettime(horas,minutos,segundos,censeg);
                     gotoxy(x+58,y-2); write(horas:2,':',minutos:2,':',segundos:2,':',censeg:2);
                    until keypressed;
                  end;
              end;
             end;
         opc:=readkey;
     end;

  Procedure Administration;

   Var
     nerfe  :salvar;
     letra  :char;
     opcion :byte;

    const
     x1 = 24;
     x2 = 58;
     y1 = 3;
     y2 = 5;


     procedure texto (seleccion:boolean; opcion:byte; x1,x2,y1,y2:byte);
       var
        opc:char;

         begin
              if seleccion then
             begin
                  x1:=x1-1;
                  x2:=x2-1;
                  y1:=y1+1;
                  y2:=y2+1;
             end
              else
             begin
                textcolor(black);
                textbackground(lightgray);
              end;

           begin
            case opcion of
              
              1:Begin
                 if seleccion then
                   begin
                     textcolor(black);
                     gotoxy(24,3); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                     gotoxy(58,4); writeln('°');
                     gotoxy(58,5); writeln('°');
                     Panel(x1,y1,x2,y2,lightgreen,black,1,false,'',' ');
                     Escribe(X1+1,Y1+1,lightgreen,black,'Recibo Telefonico');
                     gotoxy(80,1);
                   end
                 else
                   begin
                    textcolor(black);
                    gotoxy(23,6); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                    gotoxy(23,5); writeln('°');
                    gotoxy(23,4); writeln('°');
                    Panel(x1,y1,x2,y2,black,lightgray,1,true,'',' ');
                    Escribe(X1+9,Y1+1,Black,lightgray,'Resibo Telefonico');
                   end;
              end;

              2:Begin
                 if seleccion then
                   begin
                    textcolor(black);
                    gotoxy(24,11); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                    gotoxy(58,12); writeln('°');
                    gotoxy(58,13); writeln('°');
                     Panel(x1,y1+8,x2,y2+8,lightgreen,black,1,false,'',' ');
                     Escribe(X1+27,Y1+9,lightgreen,black,'Factura');
                     gotoxy(80,1);
                   end
                  else
                   begin
                    textcolor(black);
                    gotoxy(23,14); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                    gotoxy(23,13); writeln('°');
                    gotoxy(23,12);  writeln('°');
                     Panel(x1,y1+8,x2,y2+8,black,lightgray,1,True,'',' ');
                     Escribe(X1+13,Y1+9,Black,lightgray,'Factura');
                   end;
              end;

              3:Begin
                 if seleccion then
                   begin
                    textcolor(black);
                     gotoxy(24,18); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                     gotoxy(58,19); writeln('°');
                     gotoxy(58,20); writeln('°');
                     Panel(x1,y1+15,x2,y2+15,lightgreen,black,1,false,'',' ');
                     Escribe(X1+1,Y1+16,lightgreen,black,'Menu Principal');
                     gotoxy(80,1);
                   end
                  else
                   begin
                    textcolor(black);
                    gotoxy(23,21); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                    gotoxy(23,20); writeln('°');
                    gotoxy(23,19); writeln('°');
                     Panel(x1,y1+15,x2,y2+15,black,lightgray,1,True,'',' ');
                     Escribe(X1+14,Y1+16,Black,lightgray,'Salir [X]');
                   end
              end;
            end;
           end;
          end;

       procedure ejecutaropcion(opcion:byte);
         var
         opc  :char;

         begin
              case opcion of
               1:begin
                  SalvarPantalla(nerfe);
                    Telmex;
                  RestaurarPantalla(nerfe);
                end;

               2:begin
                 SalvarPantalla(nerfe);
                   factura;
                 RestaurarPantalla(nerfe);
                 end;
        end;
      end;

  begin
     
     Panel(1-1,1-1,80+1,25+1,black,lightgray,0,False,'','°');
     Panel(1,1,3,25,black,black,0,False,'',' ');
     Panel(1,24,80,25,green,black,0,False,'',' ');

     textcolor(green);
     textbackground(black);
     gotoxy(2,3); write('M');
     gotoxy(2,4); write('e');
     gotoxy(2,5); write('n');
     gotoxy(2,6); write('u');
     gotoxy(2,9); write('A');
     gotoxy(2,10); write('d');
     gotoxy(2,11); write('m');
     gotoxy(2,12); write('i');
     gotoxy(2,13); write('n');
     gotoxy(2,14); write('i');
     gotoxy(2,15); write('s');
     gotoxy(2,16); write('t');
     gotoxy(2,17); write('r');
     gotoxy(2,18); write('a');
     gotoxy(2,19); write('t');
     gotoxy(2,20); write('i');
     gotoxy(2,21); write('v');
     gotoxy(2,22); write('o');
     Escribe(53,25,green,black,'Julio Cesar Pascual Tavarez.');

     for opcion:= 1 to 3 do
         texto (false,opcion,x1,x2,y1,y2);
          opcion:=1;

   repeat
     texto(true,opcion,x1,x2,y1,y2);
     letra:=readkey;

      if letra in [#72,#75,#77,#80] then
      texto(false,opcion,x1,x2,y1,y2);

      case letra of

           #72: if opcion =1 then
                opcion:=3
                 else
           opcion:=opcion-1;

           #80: if opcion=3 then
                opcion:=1
                 else
                opcion:=opcion+1;

           #13: ejecutaropcion (opcion);
                  end;

      until (opcion=3) and (letra=#13);
    end;

  Procedure Algebra;

   Var
     nerfe  :salvar;
     letra  :char;
     opcion :byte;

    const
     x1 = 24;
     x2 = 58;
     y1 = 2;
     y2 = 4;

  Procedure circulo;

    var
       Gd, Gm         :Integer;
       x1, y1, x2, y2 :Integer;
       ch             :char;
       Radius,I       :Integer;
       radio          :integer;
       radio2         :integer;
       area,rad       :real;
       cad            :string;

begin

  Gd := Detect; InitGraph(Gd, Gm, '\tp6\bgi');
  if GraphResult <> grOk then Halt(1);

  x1 := 1;
  y1 := 1;
  x2 := 630;
  y2 := 470;

  Rectangle(0,0,Getmaxx,getmaxy);

  SetTextStyle(1,0,2);
   OutTextXY(30,40,'Radio');
   SetTextStyle(0,0,1);
   OutTextXY(82,53,'(cm.):');
   gotoxy(18,4);Readln(Radio);

    if radio > 7 then
           begin
            cleardevice;
            setcolor(white);
             outtextxy(280 ,100,'­ERROR!');
             outtextxy(193,120,'EL RADIO DEBE SER MENOR DE 7');
             outtextxy(200,140,'>REINTENTELO SI LO DESEA<');

           for i:= 1 to 25 do
             begin
               setcolor(lightgreen);
               circle((getmaxx)div(2),(getmaxy)div(2),i *2);
             END;
      end
     else
       begin

    radio2:=radio*30;

    rad:=radio*radio;
    area:=pi*rad;
    str(area:5:2,cad);

    begin
        Setcolor(4);
        setfillstyle(1,4);
        Circle(300, 240, Radio2);
        floodfill(300,240,4);
     end;


     setcolor(lightgreen);
     OutTextXY(250, 460,'Area: ');
      OutTextXY(300, 460,Cad);
       OutTextXY(500, 460,'SALIR <Esc>');
    end;

      ch:=readkey;
  CloseGraph;
  end;


   procedure cuadro;

  var
   gd,gm        :integer;
   lado,area    :longint;
   Lado2        :integer;
   tecla        :char;
   Cad          :string;
   d1,d2,d3,d4,i:integer;

  begin
   Gd := Detect; InitGraph(Gd, Gm, '\tp6\bgi');
   if GraphResult <> grOk then Halt(1);
   cleardevice;

   rectangle(1,1,getmaxX,getmaxY);

     outtextxy(10,20,'*LADO DEL CUADRO(cm.):');
        gotoxy(24,2);Read(lado);
    cleardevice;

     AREA:=LADO*LADO;

      Lado2:=lado*30;

       d1:=(640-lado2)div(2);
       d2:=d1+lado2;
       d3:=(480-Lado2)div(2);
       d4:=d3+lado2; 

       str(area:8,cad);

      rectangle(1,1,getmaxX,getmaxY);
        SetFillStyle(9,lightgreen);
         Bar(d1,d3,d2,d4);

          setcolor(lightred);
          OutTextXY(250, 470,'Area: ');
          OutTextXY(300, 470,Cad);
          setcolor(lightgreen);

          outtextxy(550,470,'[ESC] salir');  

        if lado > 15 then
           begin
            cleardevice;
            setcolor(white);
             outtextxy(280 ,100,'­ERROR!');
             outtextxy(210,120,'EL LADO DEBE SER MENOR DE 15');
             outtextxy(220,140,'>REINTENTELO SI LO DESEA<');

           for i:= 1 to 25 do
             begin
               setcolor(lightgreen);
               circle((getmaxx)div(2),(getmaxy)div(2),i *2);
             end;
          end;
        tecla:=readkey;                                                                                                                                                                                                                                                                                                                                                       
     closegraph;
  END;


 procedure rectangulo;

  var
   gd,gm        :integer;
   tecla        :char;
   Area         :longint;
   base,altura  :longint;
   base1,altura1:longint;
   Cad          :STRING;
   d1,d2,d3,d4,i:integer;

  begin
   Gd := Detect; InitGraph(Gd, Gm, '\tp6\bgi');
   if GraphResult <> grOk then Halt(1);
   cleardevice;

   rectangle(1,1,getmaxX,getmaxY);

     outtextxy(10,20,'*BASE DEL RECTAN:(cm.)');
     gotoxy(25,2);Read(base);
     outtextxy(10,35,'*ALTURA DEL RECTAN:(cm.)');
     gotoxy(26,3);Read(altura);
     cleardevice;

       BASE1:=BASE*30;
       ALTURA1:=ALTURA*30;

       AREA:=base*altura;

       d1:=(640-base1)div(2);
       d2:=d1+base1;
       d3:=(480-altura1)div(2);
       d4:=d3+altura1; 

       str(area:6,cad);

      rectangle(1,1,getmaxX,getmaxY);
        SetFillStyle(7,lightgreen);
         Bar(d1,d3,d2,d4);
          setcolor(lightred);
          OutTextXY(250, 470,'Area: ');
          OutTextXY(280, 470,Cad);

          outtextxy(550,470,'[ESC] salir');

          if base > 20 then
           begin
            cleardevice;
            SetTextStyle(0,0,1);
            setcolor(white);
             outtextxy(280 ,100,'­ERROR!');
             outtextxy(210,120,'LA BASE DEBE SER MENOR DE 20');
             outtextxy(220,140,'>REINTENTELO SI LO DESEA<');

           for i:= 1 to 25 do
             begin
               setcolor(lightgreen);
               circle((getmaxx)div(2),(getmaxy)div(2),i *2);
             end;
            end;

          if altura > 14 then
           begin
            cleardevice;
            SetTextStyle(0,0,1);
            setcolor(white);
             outtextxy(280 ,100,'­ERROR!');
             outtextxy(205,120,'LA ALTURA DEBE SER MENOR DE 14');
             outtextxy(220,140,'>REINTENTELO SI LO DESEA<');

           for i:= 1 to 25 do
             begin
               setcolor(lightgreen);
               circle((getmaxx)div(2),(getmaxy)div(2),i *2);
             end;
            end;


         if base = alTura  then
           begin
            cleardevice;
            SetTextStyle(0,0,1);
             setcolor(white);
              outtextxy(280 ,100,'­ERROR!');
              outtextxy(250,120,'SE FORMA UN CUADRO');
              outtextxy(220,140,'>REINTENTELO SI LO DESEA<');

           for i:= 1 to 25 do
             begin
               setcolor(lightgreen);
               circle((getmaxx)div(2),(getmaxy)div(2),i *2);
             end;
           end;

        tecla:=readkey;                                                                                                                                                                                                                                                                                                                                                       
     closegraph;


     END;



PROCEDURE TABLA;

     Const
       X=33;
       Y=3;

     Var
        nu      :byte;
        i,j     :integer;
        n,total :integer;
        opc     :char;
        nerfe   :salvar;
        ch      :char;

  begin
   clrscr;
   Panel(1,1,80,25,black,lightgray,2,false,'    A L G E B R A    ',' ');
   Escribe(x,y,black,lightgray,' T A B L A S');
   Escribe(x-8,y+2,black,lightgray,'- Que tabla desea consultar:  ');

   textcolor(black);
   textbackground(white);
   gotoxy(X+21,Y+2);readln(n);

   Panel(28,7,52,20,black,lightgray,1,true,'',' ');
    for i:=0 to 9 do
     begin
      j:=i+1;
      total:=j*n;
      gotoxy(X,j+8);write(j:2,' x ',n,' = ',total);
     end;
      readln;
  end;




   procedure texto (seleccion:boolean; opcion:byte; x1,x2,y1,y2:byte);
       var
        opc:char;

         begin

              if seleccion then
             begin
                  x1:=x1-1;
                  x2:=x2-1;
                  y1:=y1+1;
                  y2:=y2+1;
             end
              else
             begin
                textcolor(black);
                textbackground(lightgray);
              end;

           begin

            case opcion of
              
              1:Begin
                 if seleccion then
                   begin
                     textcolor(black);
                     gotoxy(4,2);  writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                     gotoxy(36,3); writeln('°');
                     gotoxy(36,4); writeln('°');
                     Panel(5,3,35,5,lightgreen,black,1,false,'',' ');
                     Escribe(6,4,lightgreen,black,'Rectangulo');
                     gotoxy(80,1);
                   end
                 else
                   begin
                    textcolor(black);
                    gotoxy(5,5);  writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                    gotoxy(5,4);  writeln('°');
                    gotoxy(5,3);  writeln('°');
                    Panel(6,2,36,4,black,lightgray,1,true,'',' ');
                    Escribe(16,3,Black,lightgray,'Rectangulo');
                   end;
              end;

              2:Begin
                 if seleccion then
                   begin
                    textcolor(black);
                    gotoxy(7,7);  writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                    gotoxy(40,8); writeln('°');
                    gotoxy(40,9); writeln('°');
                     Panel(9,8,39,10,lightgreen,black,1,false,'',' ');
                     Escribe(X1+9,9,lightgreen,black,'Circulo');
                     gotoxy(80,1);
                   end
                  else
                   begin
                    textcolor(black);
                    gotoxy(9,10);  writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                    gotoxy(9,9);   writeln('°');
                    gotoxy(9,8);   writeln('°');
                     Panel(10,7,40,9,black,lightgray,1,True,'',' ');
                     Escribe(X1-3,8,Black,lightgray,'Circulo');
                   end;
              end;

              3:Begin
                 if seleccion then
                   begin
                    textcolor(black);
                     gotoxy(24,12); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                     gotoxy(58,13); writeln('°');
                     gotoxy(58,14); writeln('°');
                     Panel(x1,y1+10,x2,y2+10,lightgreen,Black,1,false,'',' ');
                     Escribe(X1+1,Y1+11,lightgreen,black,'Cuadro');
                     gotoxy(80,1);
                   end
                  else
                   begin
                    textcolor(black);
                    gotoxy(23,15); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                    gotoxy(23,14); writeln('°');
                    gotoxy(23,13); writeln('°');
                     Panel(x1,y1+10,x2,y2+10,black,lightgray,1,True,'',' ');
                     Escribe(X1+14,Y1+11,Black,lightgray,'Cuadro');
                   end;
              end;

              4:Begin
                 if seleccion then
                   begin
                    textcolor(black);
                     gotoxy(10,17); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                     gotoxy(40,18); writeln('°');
                     gotoxy(40,19); writeln('°');
                     Panel(9,y1+15,39,y2+15,lightgreen,black,1,false,'',' ');
                     Escribe(X1+10,Y1+16,lightgreen,black,'Tablas');
                     gotoxy(80,1);
                   end
                  else
                   begin
                    textcolor(black);
                    gotoxy(9,20); writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                    gotoxy(9,19); writeln('°');
                    gotoxy(9,18); writeln('°');
                     Panel(10,y1+15,40,y2+15,black,lightgray,1,True,'',' ');
                     Escribe(X1-2,Y1+16,Black,lightgray,'Tablas');
                   end;
              end;


              5:Begin
                 if seleccion then
                   begin
                    textcolor(black);
                     gotoxy(6,22);   writeln('°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                     gotoxy(36,23);  writeln('°');
                     gotoxy(36,24);  writeln('°');
                     Panel(5,y1+20,35,y2+20,lightgreen,black,1,false,'',' ');
                     Escribe(X1-17,Y1+21,lightgreen,black,'Salir [X]');
                     gotoxy(80,1);
                   end
                  else
                   begin
                     escribe(5,25,black,lightgray,'°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°');
                     gotoxy(5,24);        writeln('°');
                     gotoxy(5,23);        writeln('°');
                     Panel(6,y1+20,36,y2+20,black,lightgray,1,True,'',' ');
                     Escribe(X1-9,Y1+21,Black,lightgray,'Menu Principal');

                   end;
              end;
            end;
           end;
          end;

       procedure ejecutaropcion(opcion:byte);
         var
         opc  :char;

         begin
              case opcion of
               1:begin
                  SalvarPantalla(nerfe);
                    RECTANGULO;
                  RestaurarPantalla(nerfe);
                end;

               2:begin
                 SalvarPantalla(nerfe);
                    CIRCULO;
                 RestaurarPantalla(nerfe);
                 end;

               3:begin
                 SalvarPantalla(nerfe);
                   CUADRO;
                 RestaurarPantalla(nerfe);
                 end;

               4:begin
                 SalvarPantalla(nerfe);
                   Tabla;
                 RestaurarPantalla(nerfe);
                 end;
        end;
      end;

  begin
     
     Panel(1-1,1-1,80+1,25+1,black,lightgray,0,False,'','°');
     Panel(1,1,3,25,green,black,0,False,'',' ');
            textcolor(green);
            textbackground(black);
            gotoxy(2,3); write('A');
            gotoxy(2,6); write('l');
            gotoxy(2,9); write('g');
            gotoxy(2,12); write('e');
            gotoxy(2,15); write('b');
            gotoxy(2,18); write('r');
            gotoxy(2,21); write('a');


     {Panel(39,2,41,25,Black,red,0,False,'',' ');
     Panel(1,1,2,25,Black,red,0,False,'',' ');
     Panel(25,3,25,23,Black,red,0,False,'',' ');
     Panel(55,3,55,23,Black,red,0,False,'',' ');
     Panel(79,1,80,25,Black,red,0,False,'',' ');
     Panel(1,25,80,25,white,red,0,False,'      -------- Julio Cesar Pascual Tavarez --------           ',' ');}

     for opcion:= 1 to 5 do
         texto (false,opcion,x1,x2,y1,y2);
          opcion:=1;

   repeat
     texto(true,opcion,x1,x2,y1,y2);
     letra:=readkey;

      if letra in [#72,#75,#77,#80] then
      texto(false,opcion,x1,x2,y1,y2);

      case letra of

           #72: if opcion =1 then
                opcion:=5
                 else
           opcion:=opcion-1;

           #80: if opcion=5 then
                opcion:=1
                 else
                opcion:=opcion+1;

           #13: ejecutaropcion (opcion);
                  end;

      until (opcion=5) and (letra=#13);
   end;

end.
