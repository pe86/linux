# Ανακατεύθυνση σε νέα ιστοσελίδα

Το ΠΣΔ προσφέρει τρεις βασικές μεθόδους για **hosting**:

1.  Στους παλιούς servers. Η διεύθυνση της σελίδας τότε έχει τη μορφή
    <http://12lyk-ioann.ioa.sch.gr>.
2.  Στους νέους servers (<https://webhost.sch.gr>). Η διεύθυνση της σελίδας
    τότε είναι <https://12lyk-ioann.ioa.sch.gr>. Το **"s"** σημαίνει πιο
    ασφαλής, κρυπτογραφημένη σύνδεση για τους χρήστες της σελίδας.
3.  Στο <https://blogs.sch.gr/12lykioan>. Προσοχή στη διαφορά `12lykioan`, που
    είναι σαν το username του email του σχολείου, από το `12lyk-ioann` που έχει
    παύλα `-` και πιθανώς περισσότερα γράμματα.

Η πρώτη μέθοδος δεν προτείνεται σε καμία περίπτωση. Οι servers είναι πιο αργοί,
δεν προσφέρουν τίποτα παραπάνω από τη δεύτερη περίπτωση, και δεν υπάρχει
`https`.

Η δεύτερη μέθοδος προτείνεται μόνο εφόσον δεν μας κάνει η τρίτη, και μόνο
εφόσον υπάρχει μόνιμο άτομο στο σχολείο (Πληροφορικός) που θέλει να ασχοληθεί
με συντήρηση server. Ναι μεν προσφέρεται το plesk control panel, αλλά συχνά
πυκνά θα δούμε προβλήματα *"δεν γίνεται εγκατάσταση wordpress/joomla", "δεν
είναι συμβατή η έκδοση php", "δεν παίρνει τα updates λόγω plugins", "χρειάζεται
πρόσβαση μέσω ftp"* κλπ. Δεν είναι αυτονόητο ότι όλοι οι Πληροφορικοί έχουν
χρόνο να ασχοληθούν με αυτά.

Η τρίτη μέθοδος σημαίνει ότι το ΠΣΔ συντηρεί την υποδομή και το σχολείο
συντηρεί μόνο το περιεχόμενο. Δεν χρειάζεται καμία εξειδικευμένη γνώση για τη
συντήρηση της σελίδας του σχολείου. Είναι η προτεινόμενη στις περισσότερες
περιπτώσεις.

Με βάση τα παραπάνω, κάποια σχολεία ζητούν να γίνει **redirect** από την παλιά
τους σελίδα <http://12lyk-ioann.ioa.sch.gr> στη νέα σελίδα
<https://blogs.sch.gr/12lykioan>. Για να γίνει αυτό, δημιουργήστε ένα αρχείο
`index.php`, παρόμοιο με το παρακάτω:

```php title="index.php"
<?php
  header("HTTP/1.1 301 Moved Permanently");
  header("Location: https://blogs.sch.gr/12lykioan");
  exit();
?>
```

Στη συνέχεια ανεβάστε το στην παλιά σελίδα χρησιμοποιώντας π.χ. το πρόγραμμα
`filezilla`. Αν υποθέσουμε ότι το `index.php` το έχετε στα `Έγγραφα`, ένας
γρήγορος τρόπος με [τερματικό](../../glossary/index.md#terminal) είναι:

```shell
cd ~/Έγγραφα
ftp -p users.sch.gr
username: 12lykioan
password: 1234
put index.php
bye
```
