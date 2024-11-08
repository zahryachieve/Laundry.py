# Laundry.py
Membuat Aplikasi untuk Laundry menggunakan Python
import tkinter as tk
from tkinter import messagebox

class LaundryApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Laundry App")

        # Daftar pesanan
        self.orders = []

        # Frame untuk form input
        self.input_frame = tk.Frame(self.root)
        self.input_frame.pack(padx=10, pady=10)

        # Nama pelanggan
        self.name_label = tk.Label(self.input_frame, text="Nama Pelanggan:")
        self.name_label.grid(row=0, column=0, padx=5, pady=5)
        self.name_entry = tk.Entry(self.input_frame)
        self.name_entry.grid(row=0, column=1, padx=5, pady=5)

        # Berat pakaian (kg)
        self.weight_label = tk.Label(self.input_frame, text="Berat Pakaian (kg):")
        self.weight_label.grid(row=1, column=0, padx=5, pady=5)
        self.weight_entry = tk.Entry(self.input_frame)
        self.weight_entry.grid(row=1, column=1, padx=5, pady=5)

        # Tombol tambah pesanan
        self.add_button = tk.Button(self.input_frame, text="Tambah Pesanan", command=self.add_order)
        self.add_button.grid(row=2, column=0, columnspan=2, pady=10)

        # Listbox untuk menampilkan pesanan
        self.order_listbox = tk.Listbox(self.root, width=50)
        self.order_listbox.pack(padx=10, pady=10)

        # Tombol hitung total
        self.total_button = tk.Button(self.root, text="Hitung Total", command=self.calculate_total)
        self.total_button.pack(pady=10)

    def add_order(self):
        name = self.name_entry.get()
        try:
            weight = float(self.weight_entry.get())
        except ValueError:
            messagebox.showerror("Error", "Berat pakaian harus berupa angka.")
            return

        order = f"{name} - {weight} kg"
        self.orders.append((name, weight))
        self.order_listbox.insert(tk.END, order)
        
        self.name_entry.delete(0, tk.END)
        self.weight_entry.delete(0, tk.END)

    def calculate_total(self):
        if not self.orders:
            messagebox.showinfo("Info", "Tidak ada pesanan.")
            return

        total_weight = sum(order[1] for order in self.orders)
        total_cost = total_weight * 5000  # Misalnya, biaya per kg adalah 5000

        messagebox.showinfo("Total Biaya", f"Total Biaya: Rp {total_cost:.2f}")

if __name__ == "__main__":
    root = tk.Tk()
    app = LaundryApp(root)
    root.mainloop()
