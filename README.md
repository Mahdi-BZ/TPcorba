# Corba
Exemple: Calculer un montant TTC à partir d'un montant HT et un taux de TVA en utilisant l'architecture CORBA.

exo1: simple application client/serveur CORBA. L'objet hébergé par le serveur est constitué de deux méthodes (incrementer et decrementer) définies dans l'interface IDL calcul (fichier server.idl). 


# Rapport
Realisé par : Mahdi Ben Zinouba
1. Les interactions entre le serveur et l’OA: Le serveur se charge de
a. La création des servants
b. L’enregistrement des servants au niveau de l’OA
c. Activation de l’OA
2. calculImpl hérite de la classe abstraite calculPOA et implémente les méthodes incrementer et decrementer
3. Dans les deux méthodes incrementer et decrementer on trouve le block de code suivant qui se charge de la créaction et l’émission des requêtes vers le serveur
4. Le block de code suivant se charge d’appeler les implémentations des méthodes incrementer et decrementer
org.omg.CORBA.portable.OutputStream $out = _request ("incrementer", true);
                $out.write_long (data.value);
                $in = _invoke ($out);
                data.value = $in.read_long ();
switch (__method.intValue ())
    {
       case 0:  // exo1/calcul/incrementer
       {
         org.omg.CORBA.IntHolder data = new org.omg.CORBA.IntHolder ();
         data.value = in.read_long ();
         this.incrementer (data);
         out = $rh.createReply();
         out.write_long (data.value);
break; }
       case 1:  // exo1/calcul/decrementer
       {
         org.omg.CORBA.IntHolder data = new org.omg.CORBA.IntHolder ();
         data.value = in.read_long ();
         this.decrementer (data);
         out = $rh.createReply();
         out.write_long (data.value);
break; }
default:
         throw new org.omg.CORBA.BAD_OPERATION (0,
org.omg.CORBA.CompletionStatus.COMPLETED_MAYBE);
    }
