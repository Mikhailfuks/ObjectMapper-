import Foundation

// Define a struct to represent the data to be mapped
struct Person: Codable {
  let name: String
  let age: Int
  let address: Address?
}

// Define a struct to represent nested data
struct Address: Codable {
  let street: String
  let city: String
}

// Create an ObjectMapper
let mapper = JSONDecoder()

// Sample JSON data
let jsonData = """
{
 "name": "John Doe",
 "age": 30,
 "address": {
  "street": "123 Main St",
  "city": "Anytown"
 }
}
""".data(using: .utf8)!

// Map the JSON data to a Person object
do {
 let person = try mapper.decode(Person.self, from: jsonData)
 print("Name: (person.name)")
 print("Age: (person.age)")
 print("Address: (person.address?.street ?? "N/A"), (person.address?.city ?? "N/A")")
} catch {
 print("Error mapping JSON: (error)")
}

// Map a Person object back to JSON data
let person = Person(name: "Jane Doe", age: 25, address: Address(street: "456 Elm St", city: "Sometown"))

do {
 let jsonData = try JSONEncoder().encode(person)
 let jsonString = String(data: jsonData, encoding: .utf8)!
 print("JSON: (jsonString)")
} catch {
 print("Error encoding to JSON: (error)")
}
