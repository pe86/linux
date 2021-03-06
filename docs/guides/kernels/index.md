# Πυρήνες

Για μεγαλύτερη ευστάθεια, τα πακέτα του Ubuntu λαμβάνουν ενημερώσεις ασφαλείας
και σφαλμάτων, αλλά όχι νέες εκδόσεις με νέα χαρακτηριστικά. Όμως γίνονται
εξαιρέσεις σε κάποια συγκεκριμένα πακέτα, όπως είναι ο πυρήνας (kernel). Εκεί
το Ubuntu προσφέρει δύο σειρές πακέτων (stacks), την generic (κανονική) και την
νεότερη hwe ([hardware
enablement](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)).

Όσοι κάνουν εγκατάσταση με την έκδοση 22.04 ή 22.04.1, λαμβάνουν αυτόματα τη
σειρά generic, ενώ όσοι κάνουν εγκατάσταση με την έκδοση 22.04.2 ως 22.04.5,
λαμβάνουν αυτόματα τη σειρά hwe. Οι 22.04.x εκδόσεις του Ubuntu βγαίνουν κάθε
περίπου έξι μήνες, δείτε το ακριβές χρονοδιάγραμμα
[εδώ](https://wiki.ubuntu.com/JammyJellyfish/ReleaseSchedule).

Με οποιαδήποτε έκδοση κι αν κάνετε αρχικά την εγκατάσταση, στο τέλος θα
καταλήξετε στην 22.04.5, και η μόνη διαφορά θα είναι στο αν θα έχετε το generic
ή το hwe stack, το οποίο μπορείτε έτσι κι αλλιώς να το αλλάξετε στην πορεία με
τις παρακάτω οδηγίες.

!!! warning "Προσοχή"
    Αν έχετε παλιό Ubuntu, τότε στις παρακάτω οδηγίες όπου βλέπετε την λέξη
    `linux-generic-hwe-22.04` αντικαταστήστε την με την έκδοσή σας, π.χ.
    `linux-generic-hwe-18.04`.

## Προβολή έκδοσης

Για να δείτε την έκδοση του πυρήνα που εκτελείτε μπορείτε να δώσετε `uname
-a`, ενώ για αναλυτική λίστα όλων των εμπλεκόμενων πακέτων, μπορείτε να
δώσετε:

```shell
dpkg -l | grep linux-
```

Εάν βλέπετε να περιέχουν το επίθεμα -hwe, τότε είστε στη νεότερη σειρά. Το
Ubuntu διατηρεί κάθε φορά τον τρέχοντα (π.χ. 5.15.0-25) και τον προηγούμενο
(π.χ. 5.15.0-24) πυρήνα μήπως ο τελευταίος δεν είναι εκκινήσιμος λόγω σφαλμάτων.
Εάν τυχόν έχετε πολλές εκδόσεις του ίδιου (π.χ. 5.15) πυρήνα, μπορείτε να τους
αφαιρέσετε ακολουθώντας τις οδηγίες της σελίδας
[Συντήρηση](../../ltsp/maintenance.md).

## generic

Η generic σειρά έχει το πλεονέκτημα της μεγαλύτερης σταθερότητας. Εάν το υλικό
του εργαστηρίου παίζει με αυτήν, δεν την αλλάζουμε. Για να μεταβείτε από την
hwe στην generic, δώστε:

```shell
sudo apt install linux-generic
```

Στη συνέχεια κάντε επανεκκίνηση και στο μενού ***Advanced options for Ubuntu***
του grub επιλέξτε τον προηγούμενο πυρήνα. Τέλος, δώστε:

```shell
sudo apt purge --auto-remove linux-generic-hwe-22.04
```

Εάν έχετε LTSP, κάντε και δημοσίευση εικονικού δίσκου.

## hwe

Κάποιοι πολύ νέοι υπολογιστές πιθανώς να έχουν προβλήματα με τον generic
kernel, όπως μαύρη οθόνη, χαμηλές αναλύσεις  αδυναμία εκκίνησης από το
δίκτυο... Αυτό μπορεί να συμβαίνει επειδή δεν έχουν τους απαραίτητους νέους
drivers για την κάρτα γραφικών, δικτύου κλπ. Με τη σειρά -hwe στέλνονται νέοι
πυρήνες κάθε εξάμηνο που περιέχουν τέτοιους νέους οδηγούς συσκευών, αλλά σε
μερικές περιπτώσεις μπορεί να υπάρξουν και οπισθοδρομήσεις (regressions), και
να σταματήσουν να δουλεύουν συσκευές που ήδη δουλεύανε. Γι' αυτό τον hwe kernel
τον προτιμάμε μόνο εάν διαπιστώσουμε ότι έχουμε κάποιες πολύ νέες συσκευές που
δεν λειτουργούν σωστά.

Για να εγκαταστήσετε τη hwe σειρά του πυρήνα και του xorg δώστε:

```shell
sudo apt install linux-generic-hwe-22.04
```

Στη συνέχεια κάντε επανεκκίνηση ώστε να φορτώσει ο νεότερος πυρήνας. Τέλος,
δώστε:

```shell
sudo apt purge --auto-remove linux-generic
```

Εάν έχετε LTSP, κάντε και δημοσίευση εικονικού δίσκου.
