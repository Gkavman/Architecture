# Αρχιτεκτονική Προηγμένων Υπολογιστών
## Γκαβέζος Αντώνιος, 8992

### Ερωτήματα pdf

#### 1) Βασικά χαρακτηριστικά συστήματος:
        Τύπος CPU: Atomic, Minor
        CPU Cores: 1 (Default)
        Μνήμη: 2GB (Default, εφόσον δεν πειράζουμε την παράμετρο μέσω της εντολής)
        Voltage: 3.3V
        CPU cluster Voltage: 1.2V
        CPU συχνότητα: 4GHz (Default)
        Memory Type: DDR3_1600 (Default)
        L1 & L2 type Cache
        Cache line size: 64
        
#### 2) Τα αρχεία config.ini και config.json οπως λεει και στο pdf, εκτελουν την ιδια λειτουργια απλα με διαφορετικο format. Εχουν διαφορετικο type αλλα τα αποτελεσματα παραμενουν ιδια.
        a) clock=1000
           clock=250 (4GHz)
           Type=MinorCPU
           Voltage=1.2 (Cluster) 
           Voltage=3.3 
           NumThreads=1
           Cache_line_size=64
           
        b) Αριθμος committed instructions ειναι 5028 απο το stats.txt με κωδικα:
            system.cpu_cluster.cpus.committedInsts 5028 
            (system.cpu_cluster.cpus.committedOps 5834)
        
        c) Ο συνολικος αριθμος προσπελασεων της L2 cache δινεται απο:
            system.cpu_cluster.l2.overall_accesses::total    479
  
 #### 3) Μοντελα CPU του gem5
 
         Timing Simple CPU
         Το μοντελο εχει Timing memory access. Οσον αφορα την ταχυτητα τους, ειναι πιο αργες απο τις Atomic Memory accesses αλλα παραμενει ενα γρηγορο μοντελο λογω των
         λειτουργιων του, με μονο μια εντολη να επεξεργαζεται καθε στιγμη. Το memory access απαιτει πολλους κυκλους ενω μεμονωμενες αριθμητικες πραξεις εκτελουνται σε εναν
         κυκλο. 
         
         Atomic Simple CPU
         Το μοντελο χρησιμοποιει atomic memory access δηλαδη επιτυγχανει το transaction με ενα καλεσμα της συναρτησης και επιστρεφει το αποτελεσμα μεσα απο τα function 
         returns. Χρησιμοποιουνται κυριως για cache warming και fast-forwarding λογω της δυνατοτητας τους να υπολογιζουν τον χρονο ολοκληρωσης γρηγορα και χωρις 
         καθυστερησεις. Ο AtomicSimpleCPU συνδεει τη CPU με την cache και εκτελει τις λειτουργιες που του ζητουνται σε ενα tick.
         
         Minor CPU
         Το μοντελο MinorCPU ειναι in-Order CPU με fixed pipelines και δημιουργηθηκε για ARM ISA αλλα με δυνατοτητα υποστηριξης και αλλων ISA. Αυτο που ξεχωριζει στον 
         MinorCPU ειναι τα Pipeline stages τα οποια εκτελουν διαφορετικες λειτουργιες οπως αποκωδικοποιηση ή εκτελεση εντολης. Οταν πληρουνται οι προυποθεσεις, τοτε στελνει 
         τις εντολες στο επομενο σταδιο. Τα stages επικοινωνουν για να στειλουν τα instructions, να αποφυγουν τα λαθη και να διορθωσουν τυχον σφαλμα στη σειρα εκτελεσης των 
         stages. To 4 stage pipeline αποτελειται απο:
         fetching lines, decomposition σε macro-ops, decomposition των macro-ops σε micro-ops και εκτελεση.
         
         a) MinorCPU
            sim_seconds 0.000040 #Number of seconds simulated
            
            TimingSimpleCPU
            sim_seconds 0.000045 #Number of seconds simulated
            
          b) Όπως ειδαμε και στις γενικες πληροφοριες πιο πανω, ο TimingSimpleCPU ειναι πιο αργος με πιο λεπτομερη προσβαση αρα απαιτουνται περισσοτεροι κυκλοι σε σχεση με 
          τον MinorCPU. Αυτο φαινεται και απο τους κυκλους που προσομοιωθηκαν στις δυο περιπτωσεις (TimingSimpleCPU > MinorCPU)
          
          c) 
            
            
            
            
  
