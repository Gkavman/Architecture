
# Eργαστήριο 3

# ΧΑΤΖΟΠΟΥΛΟΣ ΑΘΑΝΑΣΙΟΣ 8274
# ΓΚΑΒΕΖΟΣ ΑΝΤΩΝΙΟΣ 8992


## Μέρος Τρίτο

### Βήμα 1


	α)
		Σύμφωνα με τα όσα διαβάζουμε από το technical support paper του _McPAT_,
		ότι πρόκειται για το πρώτο ολοκληρωμένο εργαλέιο μοντελοποίησης ισχύος,
		χρόνου και χώρου ενός multithreaded πολυπύρηνου επεξεργαστή. 
		Δέχεται σαν είσοδο ειδικά δομημένα μεγάλα αρχεία XML με στόχο να παράγει στατιστικά από προσομοιώσεις της λειτουργείας 
		και απόδοσης του επεξεργαστή.
		Επιτρέπει στον χρήστη να πάρει τόσο low-level πληροφορίες αλλά και default τιμές σε high-level αρχιτεκτονικές παραμέτρους.
		Τα χαρακτηριστικά που διέπουν το εργαλείο είναι 1) η ιεραρχική μοντελοποίηση ,
		2)η βελτιοστοποίηση του καθορισμού των επιπέδων του κυκλώματος και
		3) η αναπαράσταση του εσωτερικού τσιπ για την ανάλυση των παραμέτρων του συστήματος
		
		Το εργαλείο βελτιστοποίησης εστιάζει σε δύο βασικές δομές στοιχείων: πίνακες και διασυνδέσεις. 
		Για παράδειγμα, ο χρήστης μπορεί να πειράξει την συχνότητας και την διχοτόμηση  των διασυνδέσεων ή 
		τον καθορισμό της cache της χωρητικότητας και του associativity και 
		το εργαλείο να κάνει την δουλειά για την υλοποίηση δεδομένων 
		όπως η επιλογή των μεταλικών parts η επιλογή της αποδοτικότερης καλωδίωσης του σήματος 
		και το μέγεθος των λέξεων και  bit της cache line.
		Όπως φαίνεται το εργαλείο μειώνει το χάσμα μεταξύ βελτιστοποίηση και υλοποίησης της αρχιτεκτονικής του τσιπ
		καθώς ο χρήστης μπορεί να το κλείσει και να αλλάξει την αρχιτεκτονική όπως επιθυμεί.
		Η μέγιστη ισχύς καθώς και τα στατιστικά υλοποίησης χρησιμοποιούνται μαζί με 
		έναν παράγοντα δραστηριότητας για να καθορίσουν  την τελική ισχύ κατά την εκτέλεση του προγράμματος.
		Υπάρχουν δύο φάσεις: η φάση της αρχικοποιησης και η φάση των υπολογισμών.
		Οι παράμετροι που χρησιμοποιούνται στην αρχιτεκτονική είναι παρόμοιοι με αυτούς στις προσομοιώσεις.
		Ο υπολογισμός του παράγοντα λειτουργίας της ισχύος κατά την εκτέλεση του προγράμματο δίνεται από την εξίσωση 
		
		**ActivityFactor= (AccessCount∗((n∑i=1HammingDistance)/n))/n(1)**
		
		Όπου HammingDistance το σύνολο των εναλλαγών bits μεταξύ δύο κύκλων.
		Για να απαντήσουμε σιγά σιγά και στο ερώτημα α) η συνολική ισχύς υπολογίζεται από την εξίσωση : 
		
		**Ptotal=αCVdd∆V fclk(Dynamic(+VddIshortcircuit(shortcircuit)+VddIleakage(Leakage)**
		
		Dynamic power δαπανείται για την φόρτιση και αποφόρτιση της χωρητικότητας όταν το κύκλωμα αλλάζει κατάσταση. 
		C η συνολική χωρητικότητα, Vdd η παροχή τάσης, ΔV  η διαφορά τάσης όταν αλλάζει η κατάσταση και fclk η συχνότητα ρολογιού.
		Ο παράγοντας α δείχνει τη συνολική χωρητικότητα του κυκλώματος σε έναν κύκλο ρολογιού.
		Όταν αναφερόμαστε σε leakage  μιλάμε επί της ουσίας για στατική ισχύ λόγω διαρροής ρεύματος μέσω των τρανζίστορ , 
		που στην πραγματικότητα αναφέρεται σε ατέλειες στις εναλλαγές κατάστασεις.
		Υπάρχουν  δύο διακριτοί μηχανισμοί διαρροών , το μέγεθος των οποίων είναι ανάλογο του μεγέθους των τρανζίστον 
		και εξαρτάται από την λογική κατάσταση της συσκευής.
		Ο πρώτος τύπος διαρροών ονομάζεται διαρροή κατωφλίου(Ιsub, προκαλείται όταν ένα τρανζίστορ σε κατάσταση off
		επιτρέπει μικρά ρεύματα να περνούν μεταξύ πηγής - υποδοχής και ο δεύτερος τύπος ονομάζεται διαρροής πύλης και 
		είναι οι διαρροές ρεύματος στο τερματικό της πύλης.Καθορίζεται με χρήση του εργαλείου MASTAR. 
		
		YΠολογισμός του ρεύματος διαρροής από την εξίσωση **Ιleakage=S∑s=1Pr(s)[Wsub(s)Isub+Wgon(s)Igon+Wgo f f(s)Igoff]**
		
		Βάσει των άνωθεν αναφερθέντων τμημάτων θεωρείας θεωρώ πως αν τρέξω διαφορετικά προγράμματα στον επεξεργαστή θα επηρεαστεί το  dynamic power
		καθώς θα αλλάζουν συνεχώς οι καταστάσεις και σε σταθερό fclk θα παρατηρούνται συνεχώς αλλαγές.  
		Εφόσον οι αλλαγές παρατηρούνται ανά clock cycle το μέγεθος του προγράμματος παίζει ρόλο στη διακύμανση του dynamic power 
		καθως όσο περισσότερες αλλαγές παρατηρηθούν τόσο θα μεγαλώσει η τιμή του.
	
	β) 
		Όπως αναφέρεται στο παράρτημα 4 της βιβλιογραφίας το εργαλείο McPAT μοντελοποιεί δύο κύριες τεχνικές power-saving mode: 
			1) αφαίρεση ρολογιού όταν δεν λειτουργεί το κύκλωμα για μείωση του dynamic power 
			2) power saving καταστάσεις για μείωση του static power
		Αυτό επιτρέπει στον προσομοιωτή να επηρεάζει την ισχύ και την θερμότητα των αισθητήρων , 
		με αλλαγές στα settings της συχνότητας και της τάσης , με επίκληση σε διάφορες power-saving καταστάσεις του κυκλώματος.
		Αναπτύσσονται τα P-model & C-model
			Στο P-model μειώνεται η συχνότητα ρολογίου και/ή η παρεχόμενη τάση και έτσι ο επεξεργαστή ή ο πυρήνας λειτουργεί με μικρότερο ενεργειακό προφίλ αλλά και με μικρότερη ταχύτητα επεξεργασίας. 
			Με την χρήση του McPAT ενώ λειτουργεί το κύκλωμα υπάρχει ως feedback άμεση ενημέρωση της κατανάλωσης ισχύος την συγκεκριμένη περίοδο 
			και μπορεί να γίνει κλήση του εργαλείου για προσομοίωση της ενεργού ισχύος, ώστε αν είναι επιθυμητό να αλλάξει η τάση εισόδου ή η συχνότητα ρολογιού.
			Έτσι προκύπτει ένα μοντέλο διαχείρησης ισχύος.
			Στο C-model χαρακτηρίζεται επί της ουσίας το ποσό ισχύος που καταναλείσκεται σε κάθε κατάσταση.Υπάρχουν Ν διαφορετικές C καταστάσεις με διαφορετικά power saving επίπεδα. 
			Σε κάθε μία από αυτές τις Ν καταστασεις , εκτός από την 0, μπορεί να μειωθεί δραστικά το leakage. Παρόλα αυτά δεν μπορεί να πάει πολύ βαθιά αυτό καθώς μπορεί να χαθεί χρήσιμη πληροφορία πχ από τις cache.
			To McPAT δίνει νόημα σε όλο αυτό με την χρήση πολλών sleep modes.
			O  επεξεργαστής των 40 W μπορεί να δώσει μεγαλύτερη διάρκεια ζωής στην μπαταρία βασιζόμενοι στα παραπάνω ,
			καθώς με σωστή επιλογή των παραμέτρων μπορεί να εκτελεί πιο γρήγροα λειτουργίες ενώ όταν δεν απαιτείται η χρήση του να παραμένει αδρανής.
			Τα αποτελέσματα που παράγει το McPAT μας δίνει μία ποσοστιαία εικόνα των ενεργειακών στοιχείων του επεξεργαστή 
			κατά την εκτέλεση των προγραμμάτων παρόλα αυτά είναι απαίρτητα τα δημοσιευμένα στοιχεία ενεργειακών δεδομένων του κάθε αρχείου
			ώστε να γίνει σύγκριση της διαφοράς μεταξύ της πραγματικής με την προσομοιούμενη εικόνα που παρέχει το εργαλείο.
			Αν η διαφορά μεταξύ των δύο τιμών είναι μικρή τότε μπορεί μας δώσει την απάντηση στο ερώτημα.
			
	γ)
		Από τα αποτελέσματα που παρέχει η προσομοίωση όταν τρέχω τα δύο αρχεία προκύπτει:
			H αρχική εκτίμηση και απάντηση στο ερώτημα προκύπτει με από τον πολλαπλασιασμό του runtime dynamic με τον χρόνο προσομοίωσης εκτέλεσης ενός προγράματος.
			Βλέποντας τις τιμές που δίνει το McPAT για τους δύο επεξεργαστές καταλαβαίνουμε ότι ο ΑRM  είναι περισσότερο energy efficient από τον XEON ακόμη και αν είναι 40 φορές πιο γρήγορος.
			Παρατηρώ ότι ο χώρος που απαιτεί ο ARM σε σχέση με τον Xeon είναι πολύ μικρότερος. 
			Έτσι οι ενεργειακές ανάγκες είναι πολύ μικρότερες τόσο για τη λειτουργεία του επεξεργαστή όσο και για την αλλαγή καταστάσεων και το power saving mode. 
			Παρατηρώ ότι όλες οι peak τιμές είναι πολύ μεγαλύτερες στον Xeon ,σε όλα τα επίπεδα, και επίσης οι διαρροές που παρατηρούνται στον ARM επεξεργαστή είναι πάρα πολύ μικρότερες. 
			To μικρό μέγεθος επιτρέπει καλύτερη αγωγιμότητα άρα μικρότερες διαρροές.
			Οπότε ο μεγάλος επεξεργαστής ίσως τρέξει πολύ πιο γρήγορα τις εφαρμογές ,
			παρόλα αυτά ενεργειακά ο ΑRM έχει πολύ λίγοτερες απαιτήσεις.
			Υποθέτω πως το αποτέλεσμα προκύπτει έμμεσα και με τον νόμο του Moore. 
			Ανά δύο χρόνια θα διπλασιάζονται τα τρανζίστορ άρα και η υπολογιστική ισχύς επομένως και οι ενεργειακές ανάγκες του κάθε επεξεργαστή.
			Ο XEON εχει μικροτερη καταναλωση ενεργειας την ωρα που τρεχει το προγραμμα. Δεν διακοπτεται η λειτουργια μετα την ολοκληρωση του προγραμματος. Μεγαλο 				Leakage power αρα γινεται η ARM πιο energy efficient. 	
	
#### ΜΕΡΟΣ 2ο
	
	a)
	Έγινε ανάλυση ενέργειας delay για το benchmark bzip μέσω των stats & config αρχείο που παράγει το ο gem5 και με μετατροπή μέσω της συνάρτησης 
	GEM5ToMcPAT.py παρήγαγα το αρχείο bzip_#.txt μέσω του οποίου έδινα τις απαραίτητες τιμές στην συνάρτηση print_energy.txt 
	ώστε να πάρουμε τα αρχεία bzip_#_energy.txt στα οποία αποθηκεύονται οι τιμές για energy , runtime , leakage & 
	dynamic για την συγκεκριμένη επιλογή cache , associativity etc του επεξεργαστή.
	
	Για τον BZIP : 
		
		Στην θεωρητικά βάσει CPI βέλτιστη επιλογή είχα τα εξής αποτελέσματα :
			leakage: 1.153270 W 
			dynamic: 0.310247 W 
			runtime: 0.022712 s 
			energy : 33.239398 J
			
		Στην δεύτερη κατά CPI επιλογή:
			leakage: 1.835540 W 
			dynamic: 0.215259 W 
			runtime: 0.005469 s 
			energy : 11.215820 J
		
		Για την τρίτη επιλογή:
			leakage: 1.432560 W 
			dynamic: 0.215361 W 
			runtime: 0.005466 s 
			energy : 9.007536 J
			
		Στην 4η κατά σειρά:
			leakage: 1.843780 W 
			dynamic: 0.216684 W 
			runtime: 0.005467 s 
			energy : 11.264557 J
		
		Και στην τελευταία κατά σειρά εκ των αποθηκευμένων δοκιμών(υπήρχαν και άλλες που λόγω μικρών ή καθόλου αλλαγών δεν αποθηκεύθηκαν ξεχωριστα):
			leakage: 0.729023 W 
			dynamic: 0.071853 W 
			runtime: 0.005540 s 
			energy : 4.436852 J

	Tα γινόμενα που ζητούνται είναι το EDP(ENERGY-DELAY) ΚΑΙ EDAP(ENERGY DELAY AREA)
			A) edp = 33.23 * 0.0227 = 0.745 J*s      edap = edp * coreAREA + edp * l2AREA = 1.038 + 0.557 = 1.595 J*s*mm^2
			B) edp = 11.21 * 0.0054 = 0.060534 j*s   edap = edp * coreAREA + edp * l2AREA = 0.7324 + 0.4649011 = 1.197
			C) edp = 9.00 * 0.0054 = 0.0486 j*s      edap = edp * coreAREA + edp * l2AREA = 0.471 + 0.37908= 0.850
			D) edp = 11.26 * 0.0054 = 0.060804 j*s   edap = edp * coreAREA + edp * l2AREA = 0.7726 + 0.42585 = 1.198 
			E) edp = 4.4 * 0.0055 = 0.0242 j*s       edap = edp * coreAREA + edp * l2AREA = 0.1070 + 0.05051 = 0.15 
			
	Βάση θεωρίας τα αποτελέσματα αυτά μας δίνουν χρήσιμη γνώση σχετικά με το die cost των πυρήνων του επεξεργαστή. Το εργαλείο McPAT μας δίνει εικόνα και έλεγχος βασικών στοιχείων
	ενός επεξεργαστή όπως το runtime dynamic, leakage , subthreshold leakage & short-circuit power. 
	Έχουμε εικόνα των ενεργειακών αναγκών του συστήματος σε επίπεδο ενός πυρήνα και στη συνέχεια πως διανέμεται η l2 στα threads και πως ανακτάται.
	Για παράδειγμα συνειστάται η χρήση 8πύρηνων cluster αν γίνεται ανάλυση ως προς EDP και 4 πύρηνων για EDAP 
	καθώς από μελέτες που έγιναν εκεί μειώνεται το κόστος κατασκευής προς όφελος της ταχύτητας και απόδοσης. 
	Στις δικές μας μελέτες παρατηρούμε πως παίζει ρόλο το μέγεθος της l2 και του πυρήνα καθώς είναι ανάλογα μεγέθη του  EDAP.
	
	
### Σχετικά με το ερώτημα στο τέλος:
		
		Για την τεκμηρίωση της απάντησης μου ανέτρεξα στα papers του McPAT όσο και σε online papers που βρήκα σχετικά με το θέμα και βρίσκονται στην βιβλιογραφία.
		Κατά την προσομοίωση της λειτουργείας της αρχιτεκτονικής ενός επεξεργαστή πάντα πρέπει να έχουμε τις τιμές που δημοσιοποιούνται από τον κατασκευαστή για να ξέρουμε τι απόκλισει έχουν τα αποτελέσματα μας από τα πραγματικά , 
		ώστε να προσαρμόζουμε ανάλογα και τα αποτελέσματα μας. 
		Σημαντικές αποκλίσεις προκύπτουν από πιθανές αστοχίες στην ανάπτυξη του GEM5 όπου γίνεται προσομοίωση κατά την λειτουργία ενός προγράμματος από έναν επεξεργαστή που εμείς ορίζουμε την αρχιτεκτονικής του. 
		Το εργαλείο GEM5 μας επιτρέπει να δώσουμε όποιες τιμές επιθυμούμε στα στοιχεία της δομής αλλά τα αποτελέσματα που παράγει δεν ανταποκρίνονται στην πραγματική λειτουργία.
		Αυτό το παρατηρήσαμε και στο εργαστήριο 2 που ενώ διπλασιάζαμε το ρολόι δεν πετυχαίναμε τον διπλασιασμό της ταχύτητας.
		Επίσης , όπως αναφέρει paper που χρησιμοποίησα, κατά την ομαδοποίηση των αποτελεσμάτων μεταξύ των Niagara επεξεργαστών παρατηρείται μία απόκλίση μεταξύ των δημοσιοποιημένων τιμών και αυτών του McPAT.
		Αυτό συμβαίνει γιατί το εργαλείο McPAT αγνοεί πληροφορίες (SOC LOGIC & I/O detail) οι οποίες επηρεάζουν το τελικό αποτέλεσμα.
		Επομένως όταν εμείς τρέξουμε ένα πρόγραμμα πάρουμε τα δεδομένα του GEM5 και μέσω του αρχείου GEM5ToΜcPAT 
		προσπαθήσουμε να δημιουργήσουμε το XML αρχείο που ναι απαραίτητο για την τελική προσομοίωση έχει χαθεί πληροφορία και από τα δύο εργαλεία. 
		Έτσι είναι πολύ πιθανό να υπάρχουν αποκλισεις μεταξύ προσομοιώσεων και πραγματικών συστημάτων.
		Ένας ακόμη παράγοντας είναι πως η εξακρίβωση των αποτελεσμάτων του McPAT γίνεται μόνοι μέσω των maximum τιμών των activity factors.
		Τέλος, αποτελούνται από πολύ μεγάλους κώδικες το οποίο από μόνο του μπορεί να προκαλέσει σφάλματα.
		Επίσης, οι στρογγυλοποιήσεις που γίνονται στα εργαλεία Gem5 & McPAT δεν μπορούμε να γνωρίζουμε πάντα σε πιο δεκαδικό γίνεται άρα και εκεί ενδέχεται να χάνεται πληροφορία.
		Επιπρόσθετα, βλέπουμε την προσομοιώση προγραμμάτων για λειτουργεία hardware(low level γλώσσες) από εξωμοιοτές γραμμένους σε high level γλώσσες.
		
		Kάθε πρόγραμμα κάνει την ανάλυση του βάσει την δομή στην οποία έχει ψηλότερα ιεραρχικά σημαντική για λήψη αποτελεσμάτων. 
		Πχ, το πρόγραμμα CACTΙ χρησιμοποιεί μία RAM-BASED δομή. Βασίζεται περισσότερο σε λογικές πράξεις για να δώσει το ιδανικό μέγεθος των τρανζιστορ. 
		Επίσης το πρόγραμμα  Watchh χρησιμοποιείται αρκετά , για τον υπολογισμό του dynamic power και τρέχει προσομοιώσεις αρχιτεκτονικών οι οποίες μας δείχνουν τα διάφορα εξαρτήματα και μικροελεγκτές του συστήματος.
		Μελέτες έδειξα ότι η χρήση χ86 εργαλείων παράλληλα με τον ΜcPAT σε ανάλυση προγράμματος βασισμένη σε first-order modelling είχε θετικά αποτελέσματα στα αποτελέσματα. Όσο πιο απλά τόσο καλύτερα.

### Παρατηρήσεις:
		
		Σε αυτό το εργαστήριο το δύσκολο κομμάτι ήταν η εύρεση της σύνδεσης μεταξύ των αποτελεσμάτων που παίρναμε από τα διαφόρα σημεία που ζητούνταν. 
		Επίσης ο μεγάλος όγκος δεδομένων που έπρεπε να επιλέξεις τις τιμές που οδηγούσαν στο ζητούμενο. 
		Ήταν ευχάριστο ότι στο τέλος υπήρξε εξακρίβωση αποτελεσμάτων με τα λεγόμενα ενός paper που χρησιμοποίησα για να αντλείσω πληροφορίες. 
		Παρ όλα αυτά υπήρχαν ζητήματα κυρίως λόγω της διασταύρωσης των προγραμμάτων καθώς χρειαζόταν αλλαγές στα αρχεία που κατέβασα από το git ώστε να 
		δουλέψουν ( υπήρχε εγκατεστειμένη η έκδοση python 3 & 2 ) 
		έπρεπε να γίνει αλλαγή μέσα στο GEM5TOMCPAT & PRINT_ENERGY ώστε το path να οδηγείται σε εκτέλεση 2.7. Όταν υπερνικήθηκε και αυτό το εμπόδιο η 
		διαδικασία ήταν απλή. Επίσης , ήταν κάπως δύσκολο ότι δεν δεχόταν εντολή -ο σε αρχείο bzip_energy_results και έπρεπε να τα αποθηκεύω με το χέρι.
		Παρόλα αυτά ήταν ενδιαφέρουν η εμπερία με το πρόγραμμα McPAT καθώς βλέπεις ενεργειακά τι συμβαίνει στις διασυνδέσεις των εξαρτημάτων του 
		επεξεργαστή, τις διαρροές που υπάρχουν την έκταση που θα χρειαστουν καθώς μιλάμε για ένα AREA , POWER & TIMING intergrated system. Φαντάζομαι ε
		πιτρέπει την προσομοίωση συστημάτων ώστε μετά από clustering ή scaling επιτυγχάνεται καλύτερη απόδοση με multithreading , pipeling διαδικασίες.
		Τέλος , ιδιαίτερα ενδιαφέρον ότι επιτρέπει στον κατασκευαστή να δει ποιος αριθμός πυρήνων κάνει πιο αποδοτική την αρχιτεκτονική του επεξεργαστή.
	
### Βιβλιογραφία:
		https://research.cs.wisc.edu/vertical/papers/2014/wddd-sim-harmful.pdf , https://www.hpl.hp.com/research/mcpat/micro09.pdf , 		
		https://www.samxi.org/papers/xi_hpca2015.pdf, 
		https://www.hpl.hp.com/research/mcpat/McPATAlpha_TechRep.pdf