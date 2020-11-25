# Αρχιτεκτονική Προηγμένων Υπολογιστών
## Γκαβέζος Αντώνιος, 8992

### Ερωτήματα pdf

#### 1) Βασικά χαρακτηριστικά συστήματος:
        Τύπος CPU: Atomic
        CPU Cores: 1
        Μνήμη: 2GB
        Voltage: 3.3V
        CPU cluster Voltage: 1.2V
        CPU συχνότητα: 4GHz
        Memory Type: DDR3_1600_8_X_8
        L1 & L2 type Cache
        Cache line size: 64
        
#### 2) Τα αρχεία config.ini και config.json οπως λεει και στο pdf, εκτελουν την ιδια λειτουργια απλα με διαφορετικο format. Εχουν διαφορετικο type αλλα τα αποτελεσματα παραμενουν ιδια. Ολα τα αρχεια βρεθηκαν στο αρχειο Stats.txt.
        a) clock=1000
           clock=250 (4GHz)
           Type=MinorCPU
           Voltage=1.2 (Cluster) 
           Voltage=3.3 
           NumThreads=1
           Cache_line_size=64
           Ranks per channel = 2
           
        b) Βρισκω τα αποτελεσματα απο το stats.txt με κωδικα:
            system.cpu_cluster.cpus.committedInsts 5028 #Number of Instructions committed
            system.cpu_cluster.cpus.committedOps 5834 #Number of Ops committed
            Η διαφορα των δυο αποτελεσματων οφειλεται στα micro ops που εκτελει ο gem5.
        
        c) Ο συνολικος αριθμος προσπελασεων της L2 cache δινεται απο:
            system.cpu_cluster.l2.overall_accesses::total    479
            Προκειμενου να βρω τον αριθμο των προσπελασεων της L2 Cache αν δεν παρεχοταν το αποτελεσμα απο τον εξομοιωτη, θα ανετρεχα στο αρχειο Stats.txt βρισκοντας τις
            υπολοιπες πληροφοριες οπως οι προσπελασεις της L1 cache. Μεσω hit/miss rate θα υπολογιζα τις προσπελασεις της L2 Cache.
  
 ####    Kωδικας σε C που χρησιμοποιηθηκε στον Gem5.
         
         Στοχος του script: Μια απλη προσθεση μεσα σε for loop και επιστροφη της τιμης sum.
         
         #include <stdio.h>
         int main(){
         static int sum=0 , a=0, b=0;
         for (int i=0;i<=100;i++){
                 a=a+i; b=b+2*i;
                 sum = a + b;
         }
         printf("The sum is : %d",sum);
         return sum;
         }
       
 #### 3) Συντομη περιγραφη των in-model CPUs
 
         Base Simple CPU
         O Base Simple CPU κρατάει την αρχιτεκτονική κατάσταση και διαθέτει συναρτήσεις για έλεγχο των διακοπών,στήνει ένα Fetch request , διαχειρίζεται την εκτέλεση της 
         εφαρμογής και μεταφέρει τον program counter στην επόμενη εντολή. Δεν μπορεί να τρέξει μόνο του. Η εκτέλεση του μπορεί να γίνει σε συνδυασμό με τον AtomicSimpleCPU.
 
         Timing Simple CPU
         Το μοντελο εχει Timing memory access. Οσον αφορα την ταχυτητα τους, ειναι πιο αργες απο τις Atomic Memory accesses αλλα παραμενει ενα γρηγορο μοντελο λογω των
         λειτουργιων του, με μονο μια εντολη να επεξεργαζεται καθε στιγμη. Το memory access απαιτει πολλους κυκλους ενω μεμονωμενες αριθμητικες πραξεις εκτελουνται σε εναν
         κυκλο. Διαθέτει τις ίδιες λειτουργίες με την Αtomic , και επιπρόσθετα δείχνει τις απαραίτητες συναρτήσεις για διαχείριση της ανταπόκρισης από τη μνήμη στην έξοδο.
         
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
         
####     3a) Διαφορετικα μοντελα

            MinorCPU
            
            final_tick 35069000 # Number of ticks from beginning of simulation (restored from checkpoints and never reset)
            host_inst_rate 149735 # Simulator instruction rate (inst/s)
            host_mem_usage 658284 # Number of bytes of host memory used
            host_op_rate 167885 # Simulator op (including micro ops) rate (op/s)
            host_seconds 0.07 # Real time elapsed on the host
            host_tick_rate 496225150 # Simulator tick rate (ticks/s)
            sim_freq 1000000000000 # Frequency of simulated ticks
            sim_insts 10561 # Number of instructions simulated
            sim_ops 11861 # Number of ops (including micro ops) simulated
            sim_seconds 0.000035 # Number of seconds simulated
            sim_ticks 35069000 # Number of ticks simulated
            
            
            TimingSimpleCPU
            
            final_tick 42227000 # Number of ticks from beginning of simulation (restored from checkpoints and never reset)
            host_inst_rate 120623 # Simulator instruction rate (inst/s)
            host_mem_usage 656492 # Number of bytes of host memory used
            host_op_rate 134218 # Simulator op (including micro ops) rate (op/s)
            host_seconds 0.09 # Real time elapsed on the host
            host_tick_rate 483168411 # Simulator tick rate (ticks/s)
            sim_freq 1000000000000 # Frequency of simulated ticks
            sim_insts 10529 # Number of instructions simulated
            sim_ops 11728 # Number of ops (including micro ops) simulated
            sim_seconds 0.000042 # Number of seconds simulated
            sim_ticks 42227000 # Number of ticks simulated
            
          b) Όπως ειδαμε και στις γενικες πληροφοριες πιο πανω, ο TimingSimpleCPU ειναι πιο αργος με πιο λεπτομερη προσβαση αρα απαιτουνται περισσοτεροι κυκλοι σε σχεση με 
          τον MinorCPU. Αυτο φαινεται και απο τους κυκλους που προσομοιωθηκαν στις δυο περιπτωσεις (TimingSimpleCPU > MinorCPU)
          
          c) 
            
            
            
            
  
