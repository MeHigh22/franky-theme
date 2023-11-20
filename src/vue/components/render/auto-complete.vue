<script setup>
import { ref, computed } from 'vue';
import { defineProps } from 'vue';
import {
  Combobox,
  ComboboxInput,
  ComboboxButton,
  ComboboxOptions,
  ComboboxOption,
  TransitionRoot,
} from '@headlessui/vue';
import { CheckIcon, ChevronUpDownIcon } from '@heroicons/vue/20/solid';

const breeds = [
  { label: 'Affenpinscher', value: '1' },
  { label: 'Afghaanse windhond', value: '1' },
  { label: 'Aïdi', value: '1' },
  { label: 'Airedale Terrier', value: '82' },
  { label: 'Akita', value: '1' },
  { label: 'Alaska Malamute', value: '1' },
  { label: 'Alpenländische Dachsbracke', value: '1' },
  { label: 'American Akita', value: '1' },
  { label: 'American Foxhound', value: '1' },
  { label: 'American Staffordshire Terrier', value: '1' },
  { label: 'Amerikaanse Cocker Spaniel', value: '1' },
  { label: 'Amerikaanse Water Spaniel', value: '1' },
  { label: 'Anglo-Français de Petite Vénerie', value: '1' },
  { label: 'Appenzeller Sennenhond', value: '1' },
  { label: 'Argentijnse Dog', value: '1' },
  { label: 'Ariégois', value: '1' },
  { label: 'Australian Cattle Dog', value: '1' },
  { label: 'Australian Kelpie', value: '1' },
  { label: 'Australian Shepherd', value: '1' },
  { label: 'Australian Silky Terrier', value: '1' },
  { label: 'Australian Stumpy Tail Cattle Dog', value: '1' },
  { label: 'Australian Terrier', value: '1' },
  { label: 'Azawakh', value: '1' },
  { label: 'Barbet', value: '1' },
  { label: 'Barsoi', value: '1' },
  { label: 'Basenji', value: '1' },
  { label: 'Basset Artésien Normand', value: '1' },
  { label: 'Basset Bleu de Gascogne', value: '1' },
  { label: 'Basset Fauve de Bretagne', value: '1' },
  { label: 'Basset Hound', value: '1' },
  { label: 'Bayerischer Gebirgsschweisshund', value: '1' },
  { label: 'Beagle', value: '1' },
  { label: 'Beagle Harrier', value: '1' },
  { label: 'Bearded Collie', value: '113' },
  { label: 'Beauceron', value: '1' },
  { label: 'Bedlington Terrier', value: '1' },
  { label: 'Belgische Herdershond, Groenendaeler', value: '1' },
  { label: 'Belgische Herdershond, Laekense', value: '1' },
  { label: 'Belgische Herdershond, Mechelse', value: '1' },
  { label: 'Belgische Herdershond, Tervuerense', value: '1' },
  { label: 'Bergamasco', value: '1' },
  { label: 'Berghond van de Maremmen', value: '1' },
  { label: 'Berner Laufhund', value: '1' },
  { label: 'Berner Niederlaufhund', value: '1' },
  { label: 'Berner Sennenhond', value: '1' },
  { label: 'Bischon Frise', value: '82' },
  { label: 'Billy', value: '1' },
  { label: 'Black and Tan Coonhound', value: '1' },
  { label: 'Bloedhond', value: '1' },
  { label: 'Bolognezer', value: '1' },
  { label: 'Bordeaux Dog', value: '1' },
  { label: 'Border Collie', value: '1' },
  { label: 'Border Terrier', value: '1' },
  { label: 'Bosanski Ostrodlaki Gonic Barak', value: '1' },
  { label: 'Boston Terrier', value: '1' },
  { label: 'Bouvier des Ardennes', value: '1' },
  { label: 'Bouvier des Flandres', value: '1' },
  { label: 'Boxer', value: '1' },
  { label: 'Bracco Italiano', value: '1' },
  { label: 'Brandlbracke', value: '1' },
  { label: 'Braque d\'Auvergne', value: '1' },
  { label: 'Braque de l\'Ariège', value: '1' },
  { label: 'Braque du Bourbonnais', value: '1' },
  { label: 'Braque Français, type Gascogne', value: '1' },
  { label: 'Braque Français, type Pyrénées (klein)', value: '1' },
  { label: 'Braque Saint Germain', value: '1' },
  { label: 'Braziliaanse Terrier', value: '1' },
  { label: 'Briard', value: '1' },
  { label: 'Briquet Griffon Vendéen', value: '1' },
  { label: 'Broholmer', value: '1' },
  { label: 'Bull Terrier', value: '1' },
  { label: 'Bullmastiff', value: '1' },
  { label: 'Cairn Terrier', value: '1' },
  { label: 'Canaänhond', value: '1' },
  { label: 'Cane Corso', value: '1' },
  { label: 'Cão da Serra da Estrela, korthaar', value: '1' },
  { label: 'Cão da Serra da Estrela, langhaar', value: '1' },
  { label: 'Cão da Serra de Aires', value: '1' },
  { label: 'Cão de Agua Português', value: '1' },
  { label: 'Cão de Castro Laboreiro', value: '1' },
  { label: 'Cão de Gado Transmontano', value: '1' },
  { label: 'Cão Fila de São Miguel', value: '1' },
  { label: 'Cavalier King Charles Spaniël', value: '1' },
  { label: 'Centraal-Aziatische Ovcharka', value: '1' },
  { label: 'Cesky Fousek', value: '1' },
  { label: 'Cesky Terrier', value: '1' },
  { label: 'Chart Polski', value: '1' },
  { label: 'Chesapeake Bay Retriever', value: '1' },
  { label: 'Chien d\'Artois', value: '1' },
  { label: 'Chihuahua, korthaar', value: '1' },
  { label: 'Chihuahua, langhaar', value: '1' },
  { label: 'Chinese Naakthond', value: '1' },
  { label: 'Chodsky Pes', value: '1' },
  { label: 'Chow Chow', value: '1' },
  { label: 'Cimarrón Uruguayo', value: '1' },
  { label: 'Ciobanesc Romanesc Carpatin', value: '1' },
  { label: 'Ciobanesc Romanesc de Bucovina', value: '1' },
  { label: 'Ciobanesc Romanesc Mioritic', value: '1' },
  { label: 'Cirneco dell\'Etna', value: '1' },
  { label: 'Clumber Spaniel', value: '1' },
  { label: 'Continental Bulldog', value: '1' },
  { label: 'Coton de Tuléar', value: '1' },
  { label: 'Crnogorski Planinski Gonic', value: '1' },
  { label: 'Curly Coated Retriever', value: '1' },
  { label: 'Dalmatian', value: '113' },
  { label: 'Dandie Dinmont Terrier', value: '1' },
  { label: 'Dashond, korthaar', value: '1' },
  { label: 'Dashond, langhaar', value: '1' },
  { label: 'Dashond, ruwhaar', value: '1' },
  { label: 'Daschunds', value: '82' },
  { label: 'Deens-Zweedse Boerderijhond', value: '1' },
  { label: 'Deerhound', value: '1' },
  { label: 'Dobermann', value: '1' },
  { label: 'Drentsche Patrijshond', value: '1' },
  { label: 'Drever', value: '1' },
  { label: 'Duitse Brak', value: '1' },
  { label: 'Duitse Dog, blauw', value: '1' },
  { label: 'Duitse Dog, geel/gestroomd', value: '1' },
  { label: 'Duitse Dog, zwart/zwart-wit', value: '1' },
  { label: 'Duitse Dwergpinscher', value: '1' },
  { label: 'Duitse Herdershond Langstokhaar', value: '1' },
  { label: 'Duitse Herdershond Stokhaar', value: '1' },
  { label: 'Duitse Jachtterrier', value: '1' },
  { label: 'Duitse Pinscher', value: '1' },
  { label: 'Duitse Staande Hond Draadhaar', value: '1' },
  { label: 'Duitse Staande Hond Korthaar', value: '1' },
  { label: 'Duitse Staande Hond Langhaar', value: '1' },
  { label: 'Duitse Staande Hond Stekelhaar', value: '1' },
  { label: 'Duitse Wachtelhond', value: '1' },
  { label: 'Dunker', value: '1' },
  { label: 'Dwergdashond, korthaar', value: '1' },
  { label: 'Dwergdashond, langhaar', value: '1' },
  { label: 'Dwergdashond, ruwhaar', value: '1' },
  { label: 'Dwergkeeshond', value: '1' },
  { label: 'Dwergpoedel, grijs-abrikoos-rood', value: '1' },
  { label: 'Dwergpoedel, zwart-wit-bruin', value: '1' },
  { label: 'Dwergschnauzer, peper en zout', value: '1' },
  { label: 'Dwergschnauzer, wit', value: '1' },
  { label: 'Dwergschnauzer, zwart', value: '1' },
  { label: 'Dwergschnauzer, zwart-zilver', value: '1' },
  { label: 'Eesti Hagijas', value: '1' },
  { label: 'Engelse Bulldog', value: '1' },
  { label: 'Engelse Cocker Spaniel', value: '1' },
  { label: 'Engelse Setter', value: '1' },
  { label: 'Engelse Springer Spaniel', value: '1' },
  { label: 'Engelse Toy Terrier', value: '1' },
  { label: 'English Foxhound', value: '113' },
  { label: 'Entlebucher Sennenhond', value: '1' },
  { label: 'Epagneul Bleu de Picardie', value: '1' },
  { label: 'Epagneul Breton', value: '1' },
  { label: 'Epagneul de Pont-Audemer', value: '1' },
  { label: 'Epagneul Français', value: '1' },
  { label: 'Epagneul Nain Continental, Papillon', value: '1' },
  { label: 'Epagneul Nain Continental, Phalène', value: '1' },
  { label: 'Epagneul Picard', value: '1' },
  { label: 'Erdélyi Kopo', value: '1' },
  { label: 'Eurasier', value: '1' },
  { label: 'Field Spaniel', value: '1' },
  { label: 'Fila Brasileiro', value: '1' },
  { label: 'Finse Brak', value: '1' },
  { label: 'Finse Lappenhond', value: '1' },
  { label: 'Finse Spits', value: '1' },
  { label: 'Flat-Coated Retriever', value: '113' },
  { label: 'Foxterrier Draadhaar', value: '1' },
  { label: 'Foxterrier Gladhaar', value: '1' },
  { label: 'Français Blanc et Noir', value: '1' },
  { label: 'Français Blanc et Orange', value: '1' },
  { label: 'Français Tricolore', value: '1' },
  { label: 'Franse Bulldog', value: '1' },
  { label: 'Galgo Español', value: '1' },
  { label: 'Gammel Dansk Hønsehund', value: '1' },
  { label: 'German Boxer', value: '113' },
  { label: 'Golden Retriever', value: '82' },
  { label: 'Gonczy Polski', value: '1' },
  { label: 'Gordon Setter', value: '1' },
  { label: 'Gos d\'Atura Català', value: '1' },
  { label: 'Grand Anglo-Français Blanc et Noir', value: '1' },
  { label: 'Grand Anglo-Français Blanc et Orange', value: '1' },
  { label: 'Grand Anglo-Français Tricolore', value: '1' },
  { label: 'Grand Basset Griffon Vendéen', value: '1' },
  { label: 'Grand Bleu de Gascogne', value: '1' },
  { label: 'Grand Gascon Saintongeois', value: '1' },
  { label: 'Grand Griffon vendéen', value: '1' },
  { label: 'Great Dane', value: '200' },
  { label: 'Greyhound', value: '1' },
  { label: 'Griffon belge', value: '1' },
  { label: 'Griffon Bleu de Gascogne', value: '1' },
  { label: 'Griffon bruxellois', value: '1' },
  { label: 'Griffon Fauve de Bretagne', value: '1' },
  { label: 'Griffon Korthals', value: '1' },
  { label: 'Griffon Nivernais', value: '1' },
  { label: 'Groenlandhond', value: '1' },
  { label: 'Grote Keeshond, bruin-zwart', value: '1' },
  { label: 'Grote Keeshond, wit', value: '1' },
  { label: 'Grote Keeshond, wolfsgrijs', value: '1' },
  { label: 'Grote Münsterlander', value: '1' },
  { label: 'Grote Poedel, grijs-abrikoos-rood', value: '1' },
  { label: 'Grote Poedel, zwart-wit-bruin', value: '1' },
  { label: 'Grote Zwitserse Sennenhond', value: '1' },
  { label: 'Haldenstøvare', value: '1' },
  { label: 'Hamiltonstövare', value: '1' },
  { label: 'Hannover\'scher Schweisshund', value: '1' },
  { label: 'Harrier', value: '1' },
  { label: 'Havanezer', value: '1' },
  { label: 'Heidewachtel', value: '1' },
  { label: 'Hellinikos Ichnilatis', value: '1' },
  { label: 'Hokkaido', value: '1' },
  { label: 'Hollandse Herdershond, korthaar', value: '1' },
  { label: 'Hollandse Herdershond, langhaar', value: '1' },
  { label: 'Hollandse Herdershond, ruwhaar', value: '1' },
  { label: 'Hollandse Smoushond', value: '1' },
  { label: 'Hovawart', value: '1' },
  { label: 'Hrvatski Ovcar', value: '1' },
  { label: 'Hygenhund', value: '1' },
  { label: 'Ierse rood-witte Setter', value: '1' },
  { label: 'Ierse Setter', value: '1' },
  { label: 'Ierse Terrier', value: '1' },
  { label: 'Ierse Water Spaniel', value: '1' },
  { label: 'Ierse Wolfshond', value: '1' },
  { label: 'IJslandse Hond', value: '1' },
  { label: 'Irish Glen of Imaal Terrier', value: '1' },
  { label: 'Irish Soft Coated Wheaten Terrier', value: '1' },
  { label: 'Istarski Kratkodlaki Gonic', value: '1' },
  { label: 'Istarski Ostrodlaki Gonic', value: '1' },
  { label: 'Italiaans Windhondje', value: '1' },
  { label: 'Jack Russel Terrier', value: '113' },
  { label: 'Jämthund', value: '1' },
  { label: 'Japanse Spaniel', value: '1' },
  { label: 'Japanse Spits', value: '1' },
  { label: 'Japanse Terrier', value: '1' },
  { label: 'Jura Laufhund', value: '1' },
  { label: 'Jura Niederlaufhund', value: '1' },
  { label: 'Kai', value: '1' },
  { label: 'Kangal Köpek', value: '1' },
  { label: 'Kaninchen Dashond, korthaar', value: '1' },
  { label: 'Kaninchen Dashond, langhaar', value: '1' },
  { label: 'Kaninchen Dashond, ruwhaar', value: '1' },
  { label: 'Karelische Berenhond', value: '1' },
  { label: 'Kaukasische Ovcharka', value: '1' },
  { label: 'Kerry Blue Terrier', value: '1' },
  { label: 'King Charles Spaniël', value: '1' },
  { label: 'Kintamani Bali Dog', value: '1' },
  { label: 'Kishu', value: '1' },
  { label: 'Kleine Keeshond, bruin-zwart', value: '1' },
  { label: 'Kleine Keeshond, oranje en anderskleurig', value: '1' },
  { label: 'Kleine Keeshond, wit', value: '1' },
  { label: 'Komondor', value: '1' },
  { label: 'Korea Jindo Dog', value: '1' },
  { label: 'Kraski Ovcar', value: '1' },
  { label: 'Kromfohrländer', value: '1' },
  { label: 'Kuvasz', value: '1' },
  { label: 'Labrador Retriever', value: '1' },
  { label: 'Lagotto Romagnolo', value: '1' },
  { label: 'Lakeland Terrier', value: '1' },
  { label: 'Lancashire Heeler', value: '1' },
  { label: 'Landseer ECT', value: '1' },
  { label: 'Lapinporokoira', value: '1' },
  { label: 'Leeuwhondje', value: '1' },
  { label: 'Leonberger', value: '1' },
  { label: 'Lhasa Apso', value: '1' },
  { label: 'Luzerner Laufhund', value: '1' },
  { label: 'Luzerner Niederlaufhund', value: '1' },
  { label: 'Magyar Agár', value: '1' },
  { label: 'Magyar Viszla', value: '113' },
  { label: 'Maltezer', value: '1' },
  { label: 'Manchester Terrier', value: '1' },
  { label: 'Markiesje', value: '1' },
  { label: 'Mastiff', value: '1' },
  { label: 'Mastin del Pirineo', value: '1' },
  { label: 'Mastin Español', value: '1' },
  { label: 'Mastino Napoletano', value: '1' },
  { label: 'Mexicaanse Naakthond, medio', value: '1' },
  { label: 'Mexicaanse Naakthond, miniatuur', value: '1' },
  { label: 'Mexicaanse Naakthond, standaard', value: '1' },
  { label: 'Middenslag Keeshond, bruin-zwart', value: '1' },
  { label: 'Middenslag Keeshond, oranje en anderkleurig', value: '1' },
  { label: 'Middenslag Keeshond, wit', value: '1' },
  { label: 'Middenslag Poedel, grijs-abrikoos-rood', value: '1' },
  { label: 'Middenslag Poedel, zwart-wit-bruin', value: '1' },
  { label: 'Middenslag Schnauzer, peper en zout', value: '1' },
  { label: 'Middenslag Schnauzer, zwart', value: '1' },
  { label: 'Miniature American Shepherd', value: '1' },
  { label: 'Miniatuur Bull Terrier', value: '1' },
  { label: 'Mopshond', value: '1' },
  { label: 'Mudi', value: '1' },
  { label: 'Nederlandse Kooikerhondje', value: '1' },
  { label: 'Nederlandse Schapendoes', value: '1' },
  { label: 'Newfoundland', value: '105' },
  { label: 'Newfoundlander', value: '1' },
  { label: 'Noorse Buhund', value: '1' },
  { label: 'Noorse Elandhond Grijs', value: '1' },
  { label: 'Noorse Elandhond Zwart', value: '1' },
  { label: 'Noorse Lundehund', value: '1' },
  { label: 'Norfolk Terrier', value: '1' },
  { label: 'Norrbottenspets', value: '1' },
  { label: 'Norwich Terrier', value: '1' },
  { label: 'Nova Scotia Duck Tolling Retriever', value: '1' },
  { label: 'Ogar Polski', value: '1' },
  { label: 'Old English Sheepdog', value: '1' },
  { label: 'Oostenrijkse Pinscher', value: '1' },
  { label: 'Oostsiberische Laika', value: '1' },
  { label: 'Otterhound', value: '1' },
  { label: 'Parson Russell Terrier', value: '1' },
  { label: 'Pekingees', value: '1' },
  { label: 'Perdigueiro de Burgos', value: '1' },
  { label: 'Perdigueiro Português', value: '1' },
  { label: 'Perdigueiro Português', value: '1' },
  { label: 'Perro de Agua Español', value: '1' },
  { label: 'Perro de Pastor Mallorquin', value: '1' },
  { label: 'Perro Dogo Mallorquín', value: '1' },
  { label: 'Peruaanse Naakthond, groot', value: '1' },
  { label: 'Peruaanse Naakthond, middenslag', value: '1' },
  { label: 'Peruaanse Naakthond, miniatuur', value: '1' },
  { label: 'Petit Basset griffon vendéen', value: '1' },
  { label: 'Petit Bleu de Gascogne', value: '1' },
  { label: 'Petit Brabançon', value: '1' },
  { label: 'Petit Gascon Saintongeois', value: '1' },
  { label: 'Pharaohond', value: '1' },
  { label: 'Picardische Herdershond', value: '1' },
  { label: 'Podenco Canario', value: '1' },
  { label: 'Podenco Ibicenco, gladhaar', value: '1' },
  { label: 'Podenco Ibicenco, ruwhaar', value: '1' },
  { label: 'Podengo Português, groot, gladhaar', value: '1' },
  { label: 'Podengo Português, groot, ruwhaar', value: '1' },
  { label: 'Podengo Português, klein, gladhaar', value: '1' },
  { label: 'Podengo Português, klein, ruwhaar', value: '1' },
  { label: 'Podengo Português, middenslag, gladhaar', value: '1' },
  { label: 'Podengo Português, middenslag, ruwhaar', value: '1' },
  { label: 'Poedelpointer', value: '1' },
  { label: 'Pointer', value: '1' },
  { label: 'Poitevin', value: '1' },
  { label: 'Polski Owczarek Nizinny', value: '1' },
  { label: 'Porcelaine', value: '1' },
  { label: 'Posavski Gonic', value: '1' },
  { label: 'Prazsky Krysarik', value: '1' },
  { label: 'Presa Canario', value: '1' },
  { label: 'Puli, anders dan wit', value: '1' },
  { label: 'Puli, wit', value: '1' },
  { label: 'Pumi', value: '1' },
  { label: 'Pyreneese Berghond', value: '1' },
  { label: 'Pyreneese Herdershond à face rase', value: '1' },
  { label: 'Pyreneese Herdershond à poil long', value: '1' },
  { label: 'Rafeiro do Alentejo', value: '1' },
  { label: 'Rastreador Brasileiro', value: '1' },
  { label: 'Rhodesian Ridgeback', value: '1' },
  { label: 'Riesenschnauzer, peper en zout', value: '1' },
  { label: 'Riesenschnauzer, zwart', value: '1' },
  { label: 'Riesenschnauzer, zwart zilver', value: '1' },
  { label: 'Rottweiler', value: '1' },
  { label: 'Rhodesian Ridgeback', value: '113' },
  { label: 'Russian Toy, korthaar', value: '1' },
  { label: 'Russian Toy, langhaar', value: '1' },
  { label: 'Russisch-Europese Laika', value: '1' },
  { label: 'Saarlooswolfhond', value: '1' },
  { label: 'Sabueso Español', value: '1' },
  { label: 'Saluki', value: '1' },
  { label: 'Samojeed', value: '1' },
  { label: 'Sarplaninac', value: '1' },
  { label: 'Schillerstövare', value: '1' },
  { label: 'Schipperke', value: '1' },
  { label: 'Schotse Herdershond Korthaar', value: '1' },
  { label: 'Schotse Herdershond Langhaar', value: '1' },
  { label: 'Schotse Terrier', value: '1' },
  { label: 'Schwyzer Laufhund', value: '1' },
  { label: 'Schwyzer Niederlaufhund', value: '1' },
  { label: 'Sealyham Terrier', value: '1' },
  { label: 'Segugio Italiano Gladhaar', value: '1' },
  { label: 'Segugio Italiano Ruwhaar', value: '1' },
  { label: 'Segugio Maremmano', value: '1' },
  { label: 'Shar-Pei', value: '1' },
  { label: 'Shetland Sheepdog', value: '1' },
  { label: 'Shiba', value: '1' },
  { label: 'Shih Tzu', value: '1' },
  { label: 'Shikoku', value: '1' },
  { label: 'Siberian Husky', value: '1' },
  { label: 'Sight hounds', value: '113' },
  { label: 'Sint Bernard, korthaar', value: '1' },
  { label: 'Sint Bernard, langhaar', value: '1' },
  { label: 'Skye Terrier', value: '1' },
  { label: 'Sloughi', value: '1' },
  { label: 'Slovenský Cuvac', value: '1' },
  { label: 'Slovenský Hrubosrstý Stavac', value: '1' },
  { label: 'Slovenský Kopov', value: '1' },
  { label: 'Smålandsstövare', value: '1' },
  { label: 'Small Musterlander', value: '113' },
  { label: 'Spinone Italiano', value: '1' },
  { label: 'Srpski Gonic', value: '1' },
  { label: 'Srpski Trobojni Gonic', value: '1' },
  { label: 'Stabijhoun', value: '1' },
  { label: 'Staffordshire Terrier', value: '82' },
  { label: 'Steirische ruwharige Brak', value: '1' },
  { label: 'Sussex Spaniel', value: '1' },
  { label: 'Taiwan Dog', value: '1' },
  { label: 'Tatrahond', value: '1' },
  { label: 'Thai Bangkaew Dog', value: '1' },
  { label: 'Thai Ridgeback Dog', value: '1' },
  { label: 'Tibetaanse Mastiff', value: '1' },
  { label: 'Tibetaanse Spaniel', value: '1' },
  { label: 'Tibetaanse Terrier', value: '1' },
  { label: 'Tiroler Brak', value: '1' },
  { label: 'Tornjak', value: '1' },
  { label: 'Tosa', value: '1' },
  { label: 'Toypoedel', value: '1' },
  { label: 'Tsjechoslowaakse Wolfhond', value: '1' },
  { label: 'Västgötaspets', value: '1' },
  { label: 'Vizsla Draadhaar', value: '1' },
  { label: 'Vizsla Korthaar', value: '1' },
  { label: 'Volpino Italiano', value: '1' },
  { label: 'Weimaraner, korthaar', value: '1' },
  { label: 'Weimaraner, langhaar', value: '1' },
  { label: 'Welsh Corgi Cardigan', value: '1' },
  { label: 'Welsh Corgi Pembroke', value: '1' },
  { label: 'Welsh Springer Spaniel', value: '1' },
  { label: 'Welsh Terrier', value: '1' },
  { label: 'Westhighland Terrier', value: '82' },
  { label: 'Westfaalse Dasbrak', value: '1' },
  { label: 'Westsiberische Laika', value: '1' },
  { label: 'Wetterhoun', value: '1' },
  { label: 'Whippet', value: '1' },
  { label: 'Yakutskaya Laika', value: '1' },
  { label: 'Yorkshire Terrier', value: '1' },
  { label: 'Zuid-Russische Ovcharka', value: '1' },
  { label: 'Zwart Russische Terriër', value: '1' },
  { label: 'Zweedse Lappenhond', value: '1' },
  { label: 'Zwitserse Witte Herdershond', value: '1' },
  { label: 'Other', value: '1' },
];

const selected = ref(breeds[0]);
const query = ref('');

const filteredPeople = computed(() =>
  query.value === ''
    ? breeds
    : breeds.filter((breed) => {
        return breed.label.toLowerCase().includes(query.value.toLowerCase());
      })
);

const props = defineProps(['label', 'name', 'validation']);
</script>

<template>
  <div class="increase-z">
    <Combobox v-model="selected">
      <div class="relative mt-1 mb-5">
        <label for="" class="mt-4 mb-2"> {{ label }} </label>

        <div
          class="relative w-full overflow-hidden text-left bg-white rounded-lg shadow-md cursor-default focus:outline-none focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75 focus-visible:ring-offset-2 focus-visible:ring-offset-teal-300 sm:text-sm"
        >
          <ComboboxInput
            class="w-full py-6 pl-10 pr-10 text-2xl leading-5 text-gray-900 border-none focus:ring-0"
            :displayValue="(breed) => breed.label"
            @change="query = $event.target.value"
          />
          <ComboboxButton
            class="absolute inset-y-0 right-0 flex items-center pr-2"
          >
            <ChevronUpDownIcon
              class="w-10 h-10 text-gray-400"
              aria-hidden="true"
            />
          </ComboboxButton>
        </div>
        <TransitionRoot
          leave="transition ease-in duration-100"
          leaveFrom="opacity-100"
          leaveTo="opacity-0"
          @after-leave="query = ''"
        >
          <ComboboxOptions
            class="absolute w-full py-1 mt-1 overflow-auto text-2xl bg-white rounded-md shadow-lg max-h-80 ring-1 ring-black ring-opacity-5 focus:outline-none"
          >
            <div
              v-if="filteredPeople.length === 0 && query !== ''"
              class="relative px-4 py-2 text-gray-700 cursor-default select-none"
            >
              {{ $('message.nothing_found') }}
            </div>

            <ComboboxOption
              v-for="breed in filteredPeople"
              as="template"
              :key="breed.id"
              :value="breed"
              v-slot="{ selected, active }"
            >
              <li
                class="relative py-2 pl-10 pr-4 cursor-default select-none"
                :class="{
                  'bg-[#f48f86] text-white': active,
                  'text-gray-900': !active,
                }"
              >
                <span
                  class="block truncate"
                  :class="{ 'font-medium': selected, 'font-normal': !selected }"
                >
                  {{ breed.label }}
                </span>
                <span
                  v-if="selected"
                  class="absolute inset-y-0 left-0 flex items-center pl-1"
                  :class="{ 'text-white': active, 'text-[#f48f86]': !active }"
                >
                  <CheckIcon class="h-7 w-7" aria-hidden="true" />
                </span>
              </li>
            </ComboboxOption>
          </ComboboxOptions>
        </TransitionRoot>
      </div>
    </Combobox>

    <FormKit
      type="hidden"
      disabled="true"
      v-model="selected.label"
      :label="label"
      :name="name + '_label'"
      :validation="validation"
    />

    <FormKit
      type="hidden"
      disabled="true"
      v-model="selected.value"
      :label="label"
      :name="name"
      :validation="validation"
    />
  </div>
</template>
