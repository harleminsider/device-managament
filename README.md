# device-managament
import json

class DeviceManager:
    def __init__(self, file_name="devices.json"):
        self.file_name = file_name
        self.load_devices()

    def load_devices(self):
        try:
            with open(self.file_name, "r") as file:
                self.devices = json.load(file)
        except (FileNotFoundError, json.JSONDecodeError):
            self.devices = []

    def save_devices(self):
        with open(self.file_name, "w") as file:
            json.dump(self.devices, file, indent=4)

    def add_device(self, name, category, serial_number):
        device = {
            "name": name,
            "category": category,
            "serial_number": serial_number
        }
        self.devices.append(device)
        self.save_devices()
        print(f"Device '{name}' added successfully.")

    def list_devices(self):
        if not self.devices:
            print("No devices recorded.")
            return
        for idx, device in enumerate(self.devices, start=1):
            print(f"{idx}. {device['name']} ({device['category']}) - Serial: {device['serial_number']}")

    def remove_device(self, serial_number):
        self.devices = [device for device in self.devices if device["serial_number"] != serial_number]
        self.save_devices()
        print(f"Device with serial number {serial_number} removed.")

# Example usage
def main():
    manager = DeviceManager()
    while True:
        print("\nDevice Management System")
        print("1. Add Device")
        print("2. List Devices")
        print("3. Remove Device")
        print("4. Exit")
        choice = input("Select an option: ")
        
        if choice == "1":
            name = input("Enter device name: ")
            category = input("Enter device category: ")
            serial = input("Enter serial number: ")
            manager.add_device(name, category, serial)
        elif choice == "2":
            manager.list_devices()
        elif choice == "3":
            serial = input("Enter serial number to remove: ")
            manager.remove_device(serial)
        elif choice == "4":
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
jupkjo
