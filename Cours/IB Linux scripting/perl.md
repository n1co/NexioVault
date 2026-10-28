

```perl
#!/usr/bin/perl
use strict;
use warnings;

print "Entrez un numéro de téléphone au format international français : ";
chomp(my $numero = <STDIN>);

# Expression régulière pour valider les formats :
# +336xxxxxxxx, +337xxxxxxxx, +3306xxxxxxxx, +3307xxxxxxxx
if ($numero =~ /^\+33(?:0?[67])\d{8}$/) {
    print "Numéro valide : $numero\n";
} else {
    print "Numéro invalide. Formats acceptés : +336xxxxxxxx, +337xxxxxxxx, +3306xxxxxxxx, +3307xxxxxxxx\n";
}
```


```perl
#!/usr/bin/perl
use strict;
use warnings;

my $fichier = 'log.txt';
my $erreurs = 0;

# Ouvre le fichier en lecture
open(my $fh, '<', $fichier) or die "Impossible d'ouvrir le fichier '$fichier' : $!";

while (my $ligne = <$fh>) {
    chomp($ligne);
    if ($ligne =~ /ERROR/) {
        $erreurs++;
    }
}

close($fh);

print "Nombre de lignes contenant 'ERROR' : $erreurs\n";
```


```perl
#!/usr/bin/perl
use strict;
use warnings;

# Génère un nombre aléatoire entre 1 et 100
my $secret = int(rand(100)) + 1;
my $tries = 0;

print "=== Jeu : Devine le nombre (entre 1 et 100) ===\n";

while (1) {
    print "Ta proposition : ";
    chomp(my $guess = <STDIN>);
    $tries++;

    # Vérification que l'entrée est un nombre
    if ($guess !~ /^\d+$/) {
        print "Ce n'est pas un nombre valide. Essaie encore.\n";
        next;
    }

    if ($guess < $secret) {
        print "Trop petit !\n";
    } elsif ($guess > $secret) {
        print "Trop grand !\n";
    } else {
        print "Bravo ! Tu as trouvé le nombre en $tries essai(s) !\n";
        last;
    }
}
```
