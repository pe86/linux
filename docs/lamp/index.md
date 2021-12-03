# LAMP server

Το **LAMP** είναι ένα
[αρκτικόλεξο](https://el.wikipedia.org/wiki/Αρκτικόλεξο)
το οποίο αποτελείται από τα παρακάτω συστατικά μέρη:

  - **L**: το Linux,
  - **A**: τον Apache HTTP Server,
  - **Μ**: το σύστημα διαχείρισης σχεσιακών βάσεων δεδομένων MySQL,
  - **P**: καθώς και τη γλώσσα προγραμματισμού PHP.

Ο LAMP εξυπηρετητής, ουσιαστικά είναι ένα/μια μεταπακέτο/σουίτα το οποίο
προσφέρει όλα τα απαραίτητα εργαλεία για την παροχή υπηρεσιών μέσω
διαδικτύου και είναι κατάλληλο για τη δημιουργία δυναμικών
ιστοσελίδων και διαδικτυακών εφαρμογών. Η αντίστοιχη σουίτα για
τα Windows είναι το WAMP (Windows, Apache, MySQL, PHP), για τα
Macintosh είναι το MAMP, κτλ.

## Εγκατάσταση

Η εγκατάσταση του LAMP εξυπηρετητή μπορεί να επιτευχθεί δίνοντας την
εντολή σε ένα τερματικό:

```shell
sudo apt-get install lamp-server^
```

Το μεταπακέτο `lamp-server^` εγκαθιστά όλα τα απαραίτητα πακέτα που είναι
διαθέσιμα στην τρέχουσα διανομή linux.

!!! info "Πληροφορία"
    Κατά την εγκατάσταση του μεταπακέτου θα σας ζητηθεί να δώσετε το κωδικό πρόσβασης του root χρήστης της βάσης δεδομένων.

Μετά το τέλος της εγκατάστασης, μπορείτε να μεταβείτε σε ένα
φυλλομετρητή και να δώσετε την διεύθυνση `localhost`. Εάν η εγκατάσταση
πραγματοποιήθηκε με επιτυχία θα σας εμφανιστεί το μήνυμα `It works!`

!!! tip "Συμβουλή"
    Σε περίπτωση που δεν εμφανιστεί το παραπάνω μήνυμα, δοκιμάστε να επανεκκινήσετε την υπηρεσία Apache δίνοντας σε ένα τερματικό την εντολή:

    ```shell
    sudo service apache2 restart
    ```

## Παροχή υπηρεσιών LAMP ανά χρήστη συστήματος

Για να παρέχετε σε όλους τους χρήστες του συστήματος την δυνατότητα να
μπορούν να δημιουργήσουν (πχ: PHP project) ή να εγκαταστήσουν (πχ:
Joomla, Wordpress) διάφορες υπηρεσίες διαδικτύου τοπικά στον εξυπηρετητή
θα πρέπει να ακολουθήσετε τα παρακάτω βήματα:

  - Ενεργοποίηση του `public_html` καταλόγου των χρηστών του συστήματος.
    Ο web εξυπηρετητής  δίνει την δυνατότητα στους χρήστες του
    συστήματος να διαμοιράσουν διαδικτυακά την ιστοσελίδα ή την
    υπηρεσία διαδικτύου που έχουν, μέσα από τον κατάλογο `public_html`.
    Παραδείγματος χάρη, έστω ότι έχουμε τον χρήστη συστήματος
    `administrator` με προσωπικό κατάλογο, το `/home/administrator/`.
    Εκτελώντας στον εξυπηρετητή την εντολή:

    ```shell
    sudo a2enmod userdir
    ```

    τότε ότι βρίσκεται στον κατάλογο `/home/administrator/public_html`
    θα μπορεί να προβληθεί μέσω ενός οποιοδήποτε φυλλομετρητή δίνοντας
    την διεύθυνση `<IP διεύθυνση εξυπηρετήτη>/~administrator`.

    !!! info "Πληροφορία"
        Ο κατάλογος `public_html` δεν δημιουργείται αυτόματα μετά την εκτέλεση της παραπάνω εντολής. Θα πρέπει να δημιουργηθεί από τον ίδιο τον χρήστη ή από τον διαχειριστή του συστήματος. Στην περίπτωση που δημιουργηθεί από τον διαχειριστή του συστήματος θα πρέπει μετέπειτα να εκτελεστεί η ακόλουθη εντολή:

        ```shell
        sudo chown -R <username του χρήστη>:<username του χρήστη> /home/<username του χρήστη>/public_html
        ```

  - Ενεργοποίηση της εκτέλεσης της PHP στον προσωπικό κατάλογο του
    χρήστη, εκτελώντας στον εξυπηρετητή την εντολή:

    ```shell
    sudo gedit /etc/apache2/mods-available/php5.conf
    ```

    και βάζοντας σε σχόλια τις ακόλουθες γραμμές:

    ```title="php5.conf"
    #<IfModule mod_userdir.c>
    # <Directory /home/*/public_html>
    # php_admin_value engine Off
    # </Directory>
    #</IfModule>
    ```
  
  - Επανεκκίνηση της υπηρεσίας του web εξυπηρετητή δίνοντας την
    εντολή:

    ```shell
    sudo service apache2 restart
    ```

  - Εγκατάσταση του [phpMyAdmin](phpMyAdmin.md#Εγκατάσταση).
  - Δημιουργία χρηστών στην MySQL. Σε αυτό το βήμα θα πρέπει να
    δημιουργήσετε τόσους χρήστες όσοι είναι και οι χρήστες του
    συστήματος. Για να το πετύχετε αυτό:
      - Μεταβείτε στον φυλλομετρητή και στην διεύθυνση `localhost/phpmyadmin`.
      - Κάντε κλικ στο ***Δικαιώματα***.
      - Κάντε κλικ στο ***Προσθήκη νέου χρήστη***.
      - Στην καρτέλα ***Πληροφορίες Σύνδεσης***, δώστε το επιθυμητό
        ***Όνομα χρήστη***, ***Φιλοξενητής***,
        ***Κωδικός Πρόσβασης*** και ***Επαναεισαγωγή***.

        !!! tip "Συμβουλή"
            Στο πεδίο ***Φιλοξενητής*** προτείνεται να επιλέξετε
            το ***Τοπικό***.

      - Στην καρτέλα ***Βάση δεδομένων για χρήστη***, επιλέξτε το
        ***Πλήρη δικαιώματα σε όνομα μπαλαντέρ (username\_%)***

        !!! warning "Προσοχή"
            Τα ονόματα των βάσεων δεδομένων που πρόκειται να χρησιμοποιηθούν από τις δυναμικές ιστοσελίδες του χρήστη θα πρέπει να έχουν όνομα `<username του χρήστη>_<όνομα της βάσης δεδομένων>`.
      
      - Στην καρτέλα ***Γενικά δικαιώματα***, μην επιλέξετε τίποτα.
      - Τέλος, πατήστε το ***Δημιουργία Χρήστη***.
      - Επαναλάβετε την διαδικασία και για την δημιουργία των υπολοίπων
        λογαριασμών.

  - Εγκατάσταση και παραμετροποίηση του [Proftpd FTP εξυπηρετητή]() με σκοπό την
    μεταφόρτωση αρχείων στον κατάλογο `public_html` από οποιοδήποτε υπολογιστή.