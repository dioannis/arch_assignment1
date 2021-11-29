# arch_assignment1
Αρχιτεκτονική Υπολογιστών 2021 Εργαστήριο 1

## Αρχιτεκτονική Υπολογιστών - Εργασία 1
#### Παρτσάνης Παναγιώτης - 8037
#### Διακονικολής Ιωάννης - 8802

Εκτελούμε την αρχική εντολή,
> **$ ./build/ARM/gem5.opt -d hello_result configs/example/arm/starter_se.py --cpu="minor" "tests/test-progs/hello/bin/arm/linux/hello"**

ώστε να αποθηκεύσουμε τα αποτελέσματα της προσομοίωσης στον φάκελο _hello_result_

1. **Ερώτηση 1**:
	Ανοίγουμε το **starter_se.py** αρχείο και εντοπίσαμε τα εξής χαρακτηριστικά:
	* CPU Type: MinorCPU
	* Caches:	
		* IL1 (instruction, 1st level cache memory)
		* DL1 (data, 1st level cache memory)
		* L2 (2nd level cache memory)
	*  Voltage: 3.3V
	* Clock: 1GHZ
	* Memory Mode: Timing
	* Memory Channels: 2
	* Memory Type: DDR3_1600_8x8
	* Memory Size: 2GB
2.  **Ερώτηση 2**:
	Ανοίγουμε το **stats.txt** αρχείο και βρίσκουμε:
	* _sim_seconds_ 0,000171 #_number of seconds simulated_ (τα δευτερόλεπτα της προσομοίωσης)
	* _sim_insts_ 5027 #_number of instructions simulated_ (ο αριθμός των εντολών)
	* _host_inst_rate_ 20564 #_Simulator instruction rate (inst/s)_ (ειναι τα instructions ανα δευτερολεπτο)
3. **Ερώτηση 3**:
	Βρίσκουμε πληροφορίες από τα αρχεία **stats.txt , config.ini , config.json** και συλλέγουμε τις εξής πληροφορίες:
	* IL1.miss_num = 327 (_system.cpu_cluster.cpus.icache.overall_misses::total_)
	* DL1.miss_num = 177 (_system.cpu_cluster.cpus.dcache.overall_misses::total_)
	* L2.miss_num = 474 (_system.cpu_cluster.l2.overall_misses::total_)
	* Total_Inst_num = 5027 (_sim_insts_)
	
	Στη συνέχεια, αντικαθιστούμε τις τιμές στις αντίστοιχες παραμέτρους της εξίσωσης που μας δίνεται στην εκφώνηση και βρίσκουμε: 
	**CPI = 6,316**
4. **Ερώτηση 4**:
	Συνοπτικές περιγραφές των τύπων CPU που χρησιμοποιεί ο gem5:
	* **SimpleCPU** ,είναι ένα πλήρως λειτουργικό, in-order μοντέλο που χρησιμοποιείται καλύτερα σε περιπτώσεις όπου δεν απαιτείται πολύ λεπτομέρεια, όπως warm-up periods ή απλές δοκιμές προγραμμάτων. Χωρίζεται σε 3 κλάσεις: **BaseSimpleCPU, AtomicSimpleCPU και TimingSimpleCPU**.
	* **MinorCPU**, είναι ένα επίσης in-order μοντέλο, το οποίο έχει σταθερό pipe-line και διαμορφώσιμα execute behaviours και data structures. Σκοπός του είναι να παρέχει ένα πλαίσιο για την μικρο-αρχιτεκτονική συσχέτιση του μοντέλου με συγκεκριμένους και επιλεγμένους επεξεργαστές παρόμοιων δυνατοτήτων.
**βιβλιογραφία:** 
		 * Για τον SimpleCPU: [https://www.gem5.org/documentation/general_docs/cpu_models/SimpleCPU](https://www.gem5.org/documentation/general_docs/cpu_models/SimpleCPU)
		 * Για τον MinorCPU: [https://www.gem5.org/documentation/general_docs/cpu_models/minor_cpu](https://www.gem5.org/documentation/general_docs/cpu_models/minor_cpu)

Στη συνέχεια φτιάξαμε το εξής πρόγραμμα στη C με όνομα simple.c
		



a) Με τύπο **MinorCPU** το script "se.py" εκτελέστηκε σε 0.000035s
	Με τύπο **TimingSimpleCPU** το script "se.py" εκτελέστηκε σε 0.000040s

b) Αρχικά χρησιμοποιούμε **MinorCPU** και αλλάζουμε συχνότητες.
* **MinorCPU και 10ΜHz**	
	 χρόνος εκτέλεσης: 0,000706s
* **MinorCPU και 100MHz**
	χρόνος εκτέλεσης: 0,000093s
*  **MinorCPU και 2GHz**
    χρόνος εκτέλεσης: 0,000032s

Μετά αλλάξαμε τύπο CPU:
*  **TimingSimpleCPU και 10MHz**
χρόνος εκτέλεσης: 0,000671s
*  **TimingSimpleCPU και 100MHz**
χρόνος εκτέλεσης: 0,000095s
*  **TimingSimpleCPU και2GHz**
χρόνος εκτέλεσης: 0,000037s
	 
Μετά πάλι με **MinorCPU** και αλλάζουμε μνήμες.
* **MinorCPU και DDR3**
χρόνος εκτέλεσης: 0,000035s
* **MinorCPU και DDR4_2400_8x8**
χρόνος εκτέλεσης: 0,000034s

Και τέλος αλλάζουμε τύπο CPU:
* **TimingSimpleCPU και DDR3**
χρόνος εκτέλεσης: 0,000040s
* **TimingSimpleCPU και DDR4_2400_8x8**
χρόνος εκτέλεσης: 0,000039s
