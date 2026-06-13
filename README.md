# Ananya-CHaturvedii
 import 'package:flutter/material.dart';
import 'screens/home_screen.dart';

void main() {
  runApp(const HealthcareApp());
}

class HealthcareApp extends StatelessWidget {
  const HealthcareApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Smart Healthcare',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.teal,
      ),
      home: const HomeScreen(),
    );
  }
}
class Doctor {
  final String id;
  final String name;
  final String specialty;
  final String hospital;

  Doctor({
    required this.id,
    required this.name,
    required this.specialty,
    required this.hospital,
  });
}

class Appointment {
  final String doctorName;
  final DateTime dateTime;

  Appointment({
    required this.doctorName,
    required this.dateTime,
  });
}

import 'package:flutter/material.dart';
import 'doctors_screen.dart';
import 'appointments_screen.dart';
import 'prescriptions_screen.dart';
import 'records_screen.dart';

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Smart Healthcare"),
      ),
      body: GridView.count(
        crossAxisCount: 2,
        padding: const EdgeInsets.all(16),
        children: [
          menuCard(
            context,
            "Doctors",
            Icons.medical_services,
            const DoctorsScreen(),
          ),
          menuCard(
            context,
            "Appointments",
            Icons.calendar_month,
            const AppointmentsScreen(),
          ),
          menuCard(
            context,
            "Prescriptions",
            Icons.receipt_long,
            const PrescriptionsScreen(),
          ),
          menuCard(
            context,
            "Records",
            Icons.folder,
            const RecordsScreen(),
          ),
        ],
      ),
    );
  }

  Widget menuCard(
    BuildContext context,
    String title,
    IconData icon,
    Widget page,
  ) {
    return Card(
      child: InkWell(
        onTap: () {
          Navigator.push(
            context,
            MaterialPageRoute(builder: (_) => page),
          );
        },
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Icon(icon, size: 60),
            const SizedBox(height: 10),
            Text(title),
          ],
        ),
      ),
    );
  }
}

import 'package:flutter/material.dart';

class DoctorsScreen extends StatelessWidget {
  const DoctorsScreen({super.key});

  @override
  Widget build(BuildContext context) {
    final doctors = [
      {
        "name": "Dr. Sarah Khan",
        "specialty": "Cardiologist"
      },
      {
        "name": "Dr. Amit Sharma",
        "specialty": "Dermatologist"
      },
      {
        "name": "Dr. John Lee",
        "specialty": "Neurologist"
      },
    ];

    return Scaffold(
      appBar: AppBar(
        title: const Text("Doctors"),
      ),
      body: ListView.builder(
        itemCount: doctors.length,
        itemBuilder: (context, index) {
          return ListTile(
            leading: const CircleAvatar(
              child: Icon(Icons.person),
            ),
            title: Text(doctors[index]["name"]!),
            subtitle: Text(doctors[index]["specialty"]!),
            trailing: ElevatedButton(
              onPressed: () {
                ScaffoldMessenger.of(context).showSnackBar(
                  SnackBar(
                    content: Text(
                      "Appointment booked with ${doctors[index]["name"]}",
                    ),
                  ),
                );
              },
              child: const Text("Book"),
            ),
          );
        },
      ),
    );
  }
}

import 'package:flutter/material.dart';

class RecordsScreen extends StatelessWidget {
  const RecordsScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Medical Records"),
      ),
      body: ListView(
        children: const [
          ListTile(
            leading: Icon(Icons.description),
            title: Text("Blood Test Report"),
          ),
          ListTile(
            leading: Icon(Icons.description),
            title: Text("X-Ray Scan"),
          ),
        ],
      ),
    );
  }
}
