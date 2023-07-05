import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.SerializationFeature;
import com.fasterxml.jackson.dataformat.csv.CsvMapper;
import com.fasterxml.jackson.dataformat.csv.CsvSchema;

import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

class Contact {
    private String name;
    private String email;
    private String phone;

    public Contact(String name, String email, String phone) {
        this.name = name;
        this.email = email;
        this.phone = phone;
    }

    // Getters and setters

    @Override
    public String toString() {
        return "Contact{" +
                "name='" + name + '\'' +
                ", email='" + email + '\'' +
                ", phone='" + phone + '\'' +
                '}';
    }
}

public class AddressBookIO {
    private static final String CSV_FILE_PATH = "address_book.csv";
    private static final String JSON_FILE_PATH = "address_book.json";

    public static void main(String[] args) {
        // Create sample contacts
        List<Contact> contacts = new ArrayList<>();
        contacts.add(new Contact("John Doe", "john@example.com", "1234567890"));
        contacts.add(new Contact("Jane Smith", "jane@example.com", "9876543210"));

        // Save contacts to CSV file
        saveToCsv(contacts, CSV_FILE_PATH);
        System.out.println("Contacts saved to CSV file.");

        // Read contacts from CSV file
        List<Contact> contactsFromCsv = readFromCsv(CSV_FILE_PATH);
        System.out.println("Contacts read from CSV file:");
        for (Contact contact : contactsFromCsv) {
            System.out.println(contact);
        }

        // Save contacts to JSON file
        saveToJson(contacts, JSON_FILE_PATH);
        System.out.println("Contacts saved to JSON file.");

        // Read contacts from JSON file
        List<Contact> contactsFromJson = readFromJson(JSON_FILE_PATH);
        System.out.println("Contacts read from JSON file:");
        for (Contact contact : contactsFromJson) {
            System.out.println(contact);
        }
    }

    private static void saveToCsv(List<Contact> contacts, String filePath) {
        CsvMapper csvMapper = new CsvMapper();
        CsvSchema schema = csvMapper.schemaFor(Contact.class).withHeader();
        try {
            csvMapper.writer(schema).writeValue(new File(filePath), contacts);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static List<Contact> readFromCsv(String filePath) {
        CsvMapper csvMapper = new CsvMapper();
        CsvSchema schema = CsvSchema.emptySchema().withHeader();
        List<Contact> contacts = new ArrayList<>();
        try {
            contacts = csvMapper.readerFor(Contact.class).with(schema).readValues(new File(filePath)).readAll();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return contacts;
    }

    private static void saveToJson(List<Contact> contacts, String filePath) {
        ObjectMapper objectMapper = new ObjectMapper();
        objectMapper.enable(SerializationFeature.INDENT_OUTPUT);
        try {
            objectMapper.writeValue(new File(filePath), contacts);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static List<Contact> readFromJson(String filePath) {
        ObjectMapper objectMapper = new ObjectMapper();
        List<Contact> contacts = new ArrayList<>();
        try {
            contacts = objectMapper.readValue(new File(filePath), objectMapper.getTypeFactory().constructCollectionType(List.class, Contact.class));
        } catch (IOException e) {
            e.printStackTrace();
        }
        return contacts;
    }
}
