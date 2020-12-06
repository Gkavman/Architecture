
#		ΕΡΓΑΣΤΗΡΙΟ 2 
#		ΧΑΤΖΟΠΟΥΛΟΣ ΑΘΑΝΣΙΟΣ 8274
#		ΓΚΑΒΕΖΟΣ ΑΝΤΩΝΙΟΣ 8992

## ΜΕΡΟΣ Α

### ΕΡΩΤΗΜΑ 1

	Από το αρχείο "stats.txt" μπορούν να ληφθούν σημαντικές πληροφορίες σχετικά με τα configurations των _L1 & L2 cache_.
	Πιο συγκεκριμένα και βάσει των ζητουμένων του ερωτήματος 1 του 2ου εργαστηριού μπορούμε να βρούμε για την L2:

				system.l2.demand_hits::.cpu.inst                   84                       # number of demand (read+write) hits
				system.l2.demand_hits::.cpu.data               373780                       # number of demand (read+write) hits
	
	Και για την L1:
				system.cpu.icache.demand_hits::.cpu.inst      9361832                       # number of demand (read+write) hits
				system.cpu.dcache.demand_hits::.cpu.data     48215967                       # number of demand (read+write) hits

	Σχετικά με το _associativity_ από αρχείο **config.json**:
	
	  inst l1 cache:	
			
      "path": "system.cpu.icache.tags.indexing_policy"
                            "assoc": 2
                            "entry_size": 64
                            "size": 32768
                            "addr_ranges": [
                            "0:18446744073709551615"
                            
    data l1 cache
			
      "path": "system.cpu.dcache.tags.indexing_policy"
                            "assoc": 2
                            "entry_size": 64
                            "size": 65536
                            "addr_ranges": [
                            "0:18446744073709551615"
                            
    L2 cache:
  
       "path": "system.l2.tags"
                            "assoc": 8
                            "block_size": 64
                            "addr_ranges": [
                            "0:18446744073709551615"
                            
    cache line size :

                            "cache_line_size": 64,
                
##### 2) α)
  	    
	bzip2:
			              sim_seconds                                    0.078875                       # Number of seconds simulated
                    system.cpu.cpi                                 1.577499                       # CPI: cycles per instruction
                    system.cpu.dcache.overall_miss_rate::total     0.012718                       # miss rate for overall accesses
		                system.cpu.icache.overall_miss_rate::total     0.000070                       # miss rate for overall accesses
		                system.l2.overall_miss_rate::total             0.332104                       # miss rate for overall accesses
  	   
	libm:
			              sim_seconds                                    0.175150                       # Number of seconds simulate
			              system.cpu.cpi                                 3.502995                       # CPI: cycles per instruction
			              system.cpu.dcache.overall_miss_rate::total     0.060972                       # miss rate for overall accesses
			              system.cpu.icache.overall_miss_rate::total     0.000090                       # miss rate for overall accesses
			              system.l2.overall_miss_rate::total             0.999961                       # miss rate for overall accesses
  	
	hmmer:
  	  
			              sim_seconds                                    0.070205                       # Number of seconds simulated
			              system.cpu.cpi                                 1.404099                       # CPI: cycles per instruction
			              system.cpu.dcache.overall_miss_rate::total     0.006198                       # miss rate for overall accesses
			              system.cpu.icache.overall_miss_rate::total     0.000170                       # miss rate for overall accesses
			              system.l2.overall_miss_rate::total             0.031956                       # miss rate for overall accesses
  	
	Sjeng:
			
                    sim_seconds                                     0.031043                       # Number of seconds simulated
			              system.cpu.cpi                                  1.356958                       # CPI: cycles per instruction
			              system.cpu.dcache.overall_miss_rate::total      0.003158                       # miss rate for overall accesses
			              system.cpu.icache.overall_miss_rate::total      0.005552                       # miss rate for overall accesses
			              system.l2.overall_miss_rate::total              0.982847                       # miss rate for overall accesses
  	
	mcf:
			
                    sim_seconds                                     0.007024                       # Number of seconds simulated
			              system.cpu.cpi                                  1.523883                       # CPI: cycles per instruction
			              system.cpu.dcache.overall_miss_rate::total      0.009359                       # miss rate for overall accesses
			              system.cpu.icache.overall_miss_rate::total      0.011381                       # miss rate for overall accesses
			              system.l2.overall_miss_rate::total              0.502183                       # miss rate for overall accesses
 
  
   			
#### c)
	
	Μετά την αλλαγή του clock σε 2 GHz οι τιμές γίνονται:
		
	  bzip2:
			  sim_seconds                                     0.004044                   # Number of seconds simulated

	  Πολύ μικρότερο σε σχέση με πριν

			  system.clk_domain.clock                          1000                      # Clock period in ticks

			  system.cpu_clk_domain.clock                      500                       # Clock period in ticks
  
	  Με τον όρο χρονισμό του συστήματος εννοούμε επί της ουσίας πόσο γρήγορα μπορεί να εκτελέσει το σύστημα τις εντολές που έρχονται. Αν θεωρήσουμε ως ελάχιστη μονάδα μέτρησης το ένα tick τότε σε 		
    κάθε **tick** (κύκλο ρολογιού) εκτελείται μία εργασία. Η εκτέλεση κάθε εντολής εξαρτάται από το πόσους κύκλους απαιτεί για ολοκλήρωση. Όσο πιο γρήγορο το _χτύπημα_ του ρολογιού τόσο πιο γρήγορος ο 
    υπολογιστής. Ενώ με το όρο **ρολόι** του συστήματος αναφερόμαστες στην ταχύτητα του διαύλου που μεταφέρει την εκτέλεση στη μνήμη πάνω στην μητρική πλακέτα. Έτσι με διπλασιασμό του _χρονισμού_ του 		
    επεξεργαστή επί της ουσίας υποδιπλασιάζουμε το τικ και επομένως εκτελείται πιο γρήγορα η κάθε εντολή με μείωση των κύκλων που απαιτούνται για ολοκλήρωση.
	  Πράγμα που φαίνεται και απο το αρχείο config καθώς πλέον έχουμε 2 τικ ανα κύκλο.
    Με όσα γνωρίζω από τον νόμο του Moore ανα 18-24 μήνες αλλάζουν παλι οι παράμετροι για τα τρανζιστορ του επεξεργαστή οπότε πάλι θα χρειαστεί αλλαγή των ρυθμίσεων. Οπότε αν και μπορείς με το _scaling_ να
    ενισχύσεις την απόδοση του επεξεργαστή εντούτις δεν θα λειτουργεί ες αεί οπότε δεν θεωρώ πως υπάρχει τέλειο scaling. Επίσης ο τύπους που δίνει το frequency scaling εξαρτάται από το πρόγραμμα τις εντολές
    και τον κύκλο ρολογίου, επομένως πάντα πρέπει να προσαρμόζεται σε ανάγκες και στον νόμο του Μουρ.	
  	
	
		
## ΜΕΡΟΣ 2 

### ΕΡΩΤΗΜΑ 1 

	  Όταν έτρεξα την εντολή με την επιλογές του φύλλου εργασίας το αποτέλεσμα του CPI:

			  system.cpu.cpi                               2.649110                       # CPI: cycles per instruction
	
	  α)Μετά από πολλές δοκιμές και βάσει της θεωρίας και των δεδομένων της εκφώνησης το ελάχιστον CPI για το benchmark "libm" είναι:

			  system.cpu.cpi                               2.552649                       # CPI: cycles per instruction 
		
	  β)Σχετικά με το "bzip2" benchmark μετά από πολλές δοκιμές το ελάχιστο cpi που παρατηρήθηκε ήταν:

			  system.cpu.cpi                               2.271157                       # CPI: cycles per instruction
	
	  γ) Σχετικά με το "hmmer" benchmark έπειτα από αρκετές δοκιμες το ελάχιστο cpi που παρατηρήθηκε ήταν:

			  system.cpu.cpi                               1.676712                       # CPI: cycles per instruction
	
	  δ) Όσο αφορά το "mcf" benchmark η ελάχιστη τιμή του cpi που επιτεύχθηκε ήταν:

			  system.cpu.cpi                               1.240446                       # CPI: cycles per instruction
	
	  ε) Τέλος για το benchmark "sjeng" το cpi  έφτασε σε τιμή έως:

			  system.cpu.cpi                               1.263995                       # CPI: cycles per instruction	
		
		
	  Ο τρόπος που προσέγγισα το πρόβλημα βασίζεται σε σημειώσεις του μαθήματος που είναι ανερτημένες στο elearning αλλά και έρευνα στο διαδίκτυο. Αρχικά , ένας τρόπος να βελτιωθεί η απόδοση το συστήματος είναι η μείωση των miss rate & miss penalty. Όπως αναφέρεται και 
    στις σημειώσεις 3 είδη misses αναγνωρίζονται , compulsory , capacity & conflict. Γίνεται αντιληπτό ότι πρέπει με κάποιο τρόπο να μειωθούν αυτά τα λάθη. Τα capacity προφανώς ο τρόπος να τα μειώσουμε είναι με αύξηση του μεγέθους των μνημών, βέβαια αυτό αυξάνει και 
    το κόστος που θα αναλυθεί και στο ερώτημα 3. Με αύξηση του μεγέθους του μπλοκ μπορεί να μειωθούν τα compulsory misses αλλά υπάρχει περίπτωση να έχουμε αύξηση των conflict όπου τα miss penalty είναι μεγαλύτερα και θα μειωθεί πάλι η απόδοση .
		    -Μικρότερα μπλοκ μεγαλύτερο missrate 
		    -Μεγαλύτερα μπλοκ μεγαλύτερο misspenalty ( πλεονεκτήματα spatial locality)
	 
	  Μπορούμε να αυξήσουμε το associativity , που όπως λέει ο 2:1 thumb rule  μία DMA cache N size έχει ίδιο miss rate με μία 2 way N/2 size cache. Βέβαια και σε αυτό υπάρχει πρόβλημα καθώς μεγαλύτερο assoc σημαίνει περισσότερο hardware άρα και αύξηση κόστους-πολυπλοκότητας. 
	  Ένας ακόμη τρόπος που δεν θεωρώ πως διορθωνεται στην εργασία μας αλλά είναι ιδιαίτερα χρήσιμος έχει να κάνει με hardware prefetching. Όπου επί της ουσίας δεδομένα καλούνται πριν ζητηθούν από το πρόγραμμα. Επίσης η δημιουργία virtual memory. 
	  Σε ένα σύστημα 2-επιπέδων cache ο AMAT(Average memory access time) = L1 HT + L1 MR × (L2 HT + L2 MR × L2 MP) . Αν θεωρήσουμε ότι γνωρίζουμε τα ΜΡ για εντολές δεδομένων(ld,st) και ή απλές εντολές(add, sub ) μπορούμε να προσαρμόσουμε τα μεγέθη των dcache , icache , l2 cache ,
    cache line size και associativy  ώστε η προέκταση της από πάνω εξίσωσης που συνδέεται άμεσα με το   CPI να παίρνει όσο δυνατόν μικρότερες τιμές.  
	  Βασίστηκα σε όλα τα προαναφερθέντα ώστε να προσαρμόσω καλύτερα τις τιμές των configurable στοιχείων ώστε να ληφθούν τα άνωθεν αποτελέσματα. 
    Λόγω προβλήματος με την εφαρμογή των γραφημάτων δεν μπόρεσα να βγάλω αντίστοιχα γραφήματα για το ερώτημα β οπότε δημιούργησα τα αρχεία txt για κάθε benchmark με επαρκή σχόλια για αποσαφήνιση της συλλογιστικής πορείας για μείωση του cpi.
	

###	ΕΡΩΤΗΜΑ 3

	  Αν θεωρήσουμε μία ιδεατή μονάδα μέτρησης κόστους. Αυτή εξαρτάται από το μέγεθος των μνημών cache , από το συνολικό hardware που θα απαιτηθεί για την εξυπηρέτηση των αναγκών του συστήματος , το σύστημα θα αναπτυχθεί ως set associative που σημαίνει ότι όσο μεγαλώνει το associativity
    μεγαλώνει η πολυπλοκότητα άρα και οι υλικές ανάγκες του συστήματος(κόστος). Επίσης 
	
			  Κόστος = _HARDWARE_FOR_ASSOCIATIVITY_+BLOCK_SIZE + L1 CACHE SIZE + L2 CACHE SIZE
	
	  Όπου:
			  L1 CACHE SIZE COST = L1 DATA CACHE SIZE COST + L1 INSTRUCTION CACHE SIZE COST 
					  Aυξανομένου μεγέθους αυξάνεται το κόστος.
			  L2 CACHE SIZE COST : Όσο μεγαλύτερο τόσο πιο κοστοβόρο.
		
    Σε κάθε περίπτωση το κόστης της L1 είναι μεγαλύτερο από της  L2 , όμως ο χρόνος που θα απαιτηθεί και το misspenalty στην L2 είναι μεγαλύτερο απ' ότι στην L1 (προκύπτει από θεωρία και αποτελέσματα β μέρους) . Οπότε πρέπει να κάνουμε σωστή επιλογή των μεγεθών ώστε να παίρνουμε όσο δυνατόν
    ταχύτερη ανάκτηση πληροφορίας  με το μικρότερο δυνατό κόστης ανάπτυξης.
	  Όσο μεγαλύτερο το block size τόσο μικρότερο το miss rate όμως με αυξανόμενο miss penalty.
    Τέλος όσο αυξάνουμε το associativity τόσο μεγαλώνει και ο χρόνος προσπέλασης.
	  Με όλα αυτά τα στοιχεία και τα δεδομένα από τα αποτελέσματα του μέρους 2 μπορούμε να θεωρήσουμε πως υπάρχει ένα ιδανικό block size ανάλογα με τα μεγέθη των cache μνημών όπου με σωστή επιλογή του associativity μπορούμε να πάρουμε ταχύτερο cpi και να κάνουμε πιο γρήγορο το ΑΜΑΤ. 
	  Η δική μου υπόθεση είναι πως για σχετικά μικρές l1 (data & instruction) αλλά θεωρητικά μεγάλες τιμές της l2 (2MB) l1d_assoc = 2 & l1i_assoc=2 , l2_assoc=4/8 για ένα cache line size = 64 βελτιστοποιείται η διαδικασία έχοντας παράλληλα χαμηλό κόστος κατασκευής.
		
### ΠΑΡΑΤΗΡΗΣΕΙΣ ΠΑΝΩ ΣΤΟ ΕΡΓΑΣΤΗΡΙΟ 2

		Στο σημείο αυτό θα ήθελα να παραθέσω τις δυσκολίες, σκέψεις και ένα feedback από την ενασχόληση μου με αυτό το εργαστήριο. 
		Αρχικά, ο τρόπος που προσπάθησα να εκτελέσω τα βήματα ήταν πολύ πιο οικείoς σε σχέση με το πρώτο εργαστήριο, καθώς υπήρχε μία εξοικείωση.
		Παρ' όλα αυτά υπήρξε ένα πρόβλημα που με ταλαιπώρησε και έχει να κάνει με το benchmark "hmmer" όπου η εντολή -seed ετρεχε στο bash μου ως --seed και μου πήρε κάποιο χρόνο να το βρω στο διαδίκτυο.
		Έπειτα , ανέφερα και στην αναφορά παραπάνω πως είχα θέμα με την δημιουργία γραφημάτων καθώς δεν μπορούσα να τα κάνω  copy paste από τα windows και στο ubuntu τα έβγαζε κάπως περίεργα, ενω τα δεδομενα του βηματος 2.2 δεν τα εβγαζε καθολου.
		Παρόλα αυτά βρήκα ιδιαίτερα ενδιαφέρον το ότι μπορείς μέσα από θεωρητικές εξομοιώσεις της λειτουργίας ενός επεξεργαστή ότι μπορείς να πάρεις χρήσιμα δεδομένα για το πώς μπορείς να βελτιώσεις την απόδοση του και τι κόστος έχει κάθε επιλογή σου τόσο σε χρόνο όσο και σε πολυπλοκότητα - χρήμα.
		Ένα κομμάτι που με δυσκόλεψε και είχε αναφερθεί από την πρώτη στιγμή ήταν ο χρόνος που απαιτείται ώστε να τρέξουν τα  benchmarks.
		Όταν άρχισα να καταλαβαίνω τα αποτελέσματα κάθε κλήσης άρχισα να αλλάζω της προυποθέσης εκτέλεσης τους ώστε σε μικρότερο χρόνο να βλέπεις αν οι αλλαγές έχουν θετικό ή αρνητικό αντίκτυπο στο Cpi.
		Τέλος, ήταν πολύ χρήσιμο το script για αποθήκευση των stats που επιθυμώ καθώς έτσι είχα πιο γρήγορη και ολοκληρωμένη οπτική αν οι αλλαγές που κάνω οδηγούν στο επιθυμητό αποτέλεσμα.
		
		
# ΒΙΒΛΙΟΓΡΑΦΙΑ
		http://learning.gem5.org/book/part1/gem5_stats.html ,
		https://www.gem5.org/documentation/general_docs/memory_system/gem5_memory_system/ ,
		https://www.extremetech.com/extreme/188776-how-l1-and-l2-cpu-caches-work-and-why-theyre-an-essential-part-of-modern-chips , 
		https://stackoverflow.com/questions/59479336/calculating-cpi-for-2-cache-level ,
		http://home.ku.edu.tr/comp303/public_html/Lecture15.pdf , 
		https://en.wikipedia.org/wiki/Frequency_scaling ,
		http://www.it.uom.gr/project/mycomputer/cpu/info/eks_leit.html , 
		http://ece-research.unm.edu/jimp/611/slides/chap5_2.html ,
		https://eecs.oregonstate.edu/research/vlsi/teaching/ECE472_FA12/Chapter5_FINAL_ASSOC_VM.pdf
