# Python HTTP server

Ένας γρήγορος τρόπος να μοιράσουμε HTML ή άλλα αρχεία στο τοπικό δίκτυο είναι
να ανοίξουμε το πρόγραμμα διαχείρισης αρχείων, να κάνουμε ***δεξί κλικ*** ▸
***Άνοιγμα σε Τερματικό*** πάνω στον κατάλογο που μας ενδιαφέρει, και από εκεί
να τρέξουμε την παρακάτω εντολή:

```shell
python3 -m http.server
```

Έτσι ξεκινά ένας μικρός **web server** ο οποίος σερβίρει τα περιεχόμενα του
τρέχοντος καταλόγου στο δίκτυο. Επειδή από προεπιλογής χρησιμοποιεί τη θύρα
**8000**, δεν συγκρούεται με άλλους web servers που πιθανώς να έχουμε
εγκατεστημένους. Στη συνέχεια, στους clients αν ανοίξουμε έναν browser και
επισκεφθούμε τη διεύθυνση <http://server-ip:8000>, θα δούμε μια ιστοσελίδα σαν
την παρακάτω:

!!! quote "Directory listing for /"
    - index.html
    - win32-loader
    - other-files...

Από εκεί με ***δεξί κλικ*** ▸ ***Αποθήκευση συνδέσμου ως*** μπορούμε να
αποθηκεύσουμε τα αρχεία στο δίσκο, ή με ***αριστερό κλικ*** μπορούμε να τα
δούμε απευθείας εφόσον είναι αρχεία .html.

!!! info "Πληροφορία"
    Μια παρόμοια εντολή είναι και η `php -S 0.0.0.0:8000`, με τις διαφορές ότι
    δεν δείχνει λίστα αρχείων (θα πρέπει να γράψουμε το πλήρες URL), και ότι
    επιτρέπει την εκτέλεση αρχείων php.
