import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Material App',
      home: Scaffold(
          appBar: AppBar(
            title: Text('Jheri (5SIA1)'),
          ),
          body: MyList()),
    );
  }
}

class MyList extends StatefulWidget {
  @override
  _MyListState createState() => _MyListState();
}

class _MyListState extends State<MyList> {
  final List<Anime> anime = AnimeList.getAnime();

  Widget build(BuildContext context) {
    return Container(
      child: anime.length > 0
          ? ListView.builder(
              itemCount: anime.length,
              itemBuilder: (BuildContext context, int index) {
                return Dismissible(
                  onDismissed: (DismissDirection direction) {
                    setState(() {
                      anime.removeAt(index);
                    });
                  },
                  secondaryBackground: Container(
                    child: Center(
                      child: Text(
                        'Delete',
                        style: TextStyle(color: Colors.white),
                      ),
                    ),
                    color: Colors.red,
                  ),
                  background: Container(),
                  child: AnimeCard(anime: anime[index]),
                  key: UniqueKey(),
                  direction: DismissDirection.endToStart,
                );
              },
            )
          : Center(child: Text('No Items')),
    );
  }
}

// Objek Model
class Anime {
  String judul;
  String namapengarang;
  String skor;
  String fotoURL;

  Anime({this.judul, this.namapengarang, this.skor, this.fotoURL});
}

// Objek Data
class AnimeList {
  static List<Anime> getAnime() {
    return [
      Anime(
          judul: 'NARUTO SHIPPUDEN',
          namapengarang: 'Masashi Kishimoto',
          skor: 'Skor MAL\n82,5',
          fotoURL:
              'https://cdn.idntimes.com/content-images/community/2020/03/uzumaki-naruto-1-25ad72624f53230e0ffeb1c57ed39c3f_wm_600x315.jpg'),
      Anime(
          judul: 'ONE PIECE',
          namapengarang: 'Eiichiro Oda',
          skor: 'Skor MAL\n90',
          fotoURL:
              'https://upload.wikimedia.org/wikipedia/en/9/90/One_Piece%2C_Volume_61_Cover_%28Japanese%29.jpg'),
      Anime(
          judul: 'Tensei Shitara Slime Datta Ken',
          namapengarang: 'Fuse',
          skor: 'Skor MAL\n75',
          fotoURL:
              ''),
      Anime(
          judul: 'DRIFTERS',
          namapengarang: 'Kouta Hirano',
          skor: 'Skor MAL\n80,5',
          fotoURL:
              ''),
      ];
  }
}

//Objek View
class AnimeCard extends StatelessWidget {
  final Anime anime;

  AnimeCard({this.anime});

  Widget build(BuildContext context) {
    return Card(
      child: Column(
        children: <Widget>[
          ListTile(
            leading: CircleAvatar(
              backgroundImage: NetworkImage(anime.fotoURL),
            ),
            title: Text(anime.judul),
            subtitle: Text(anime.namapengarang),
            trailing: Text(anime.skor),
          )
        ],
      ),
    );
  }
}
