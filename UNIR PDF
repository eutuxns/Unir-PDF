# 1. Se deben instalar las librerias 
# pip install openpyxl
# pip install pyinstaller

# 2. Se genera un archivo con extension .py

# 3. Se abre el CMD
# Nota: Se puede abrir el de la computadora, pero para mayor facilidad también se puede abrir el local en el compilador de preferencia

# 4. Se ejecuta
# cd + ruta donde este el archivo de python .py


# 5. Se ejecuta la instruccion 
# pyinstaller --onefile --noconsole NOMBRE_DEL_ARCHIVO.py


import fitz  # PyMuPDF
import tkinter as tk
from tkinter import filedialog, messagebox

class PDFMergerApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Unir PDFs")
        self.root.geometry("400x200")
        self.root.configure(bg="#D8BFD8")  # Fondo lila
        
        # Lista para almacenar archivos PDF seleccionados
        self.pdf_files = []

        # Crear botones
        self.load_button = tk.Button(
            root, text="Cargar PDFs", command=self.load_pdfs,
            bg="#9370DB", fg="white", font=("Arial", 12), padx=10, pady=5
        )
        self.load_button.pack(pady=10)

        self.merge_button = tk.Button(
            root, text="Juntar PDFs", command=self.merge_pdfs,
            bg="#9370DB", fg="white", font=("Arial", 12), padx=10, pady=5
        )
        self.merge_button.pack(pady=10)

        self.save_button = tk.Button(
            root, text="Descargar", command=self.save_pdf,
            bg="#9370DB", fg="white", font=("Arial", 12), padx=10, pady=5
        )
        self.save_button.pack(pady=10)

    def load_pdfs(self):
        """Cargar múltiples archivos PDF."""
        files = filedialog.askopenfilenames(
            title="Seleccionar PDFs",
            filetypes=[("Archivos PDF", "*.pdf")]
        )
        if files:
            self.pdf_files = list(files)
            messagebox.showinfo("Cargar PDFs", f"Se seleccionaron {len(self.pdf_files)} archivos.")

    def merge_pdfs(self):
        """Unir archivos PDF seleccionados."""
        if not self.pdf_files:
            messagebox.showwarning("Advertencia", "No se han cargado archivos PDF.")
            return
        
        # Crear un objeto PDF vacío
        self.merged_pdf = fitz.open()

        # Unir los PDFs seleccionados
        try:
            for pdf in self.pdf_files:
                with fitz.open(pdf) as doc:
                    for page in doc:
                        self.merged_pdf.insert_pdf(doc)
            messagebox.showinfo("Juntar PDFs", "Los PDFs se unieron exitosamente.")
        except Exception as e:
            messagebox.showerror("Error", f"Error al juntar PDFs: {e}")

    def save_pdf(self):
        """Guardar el archivo PDF unido."""
        if not hasattr(self, "merged_pdf") or not len(self.merged_pdf):
            messagebox.showwarning("Advertencia", "No hay un archivo unido para guardar.")
            return
        
        output_path = filedialog.asksaveasfilename(
            title="Guardar archivo PDF",
            defaultextension=".pdf",
            filetypes=[("Archivos PDF", "*.pdf")]
        )
        if output_path:
            try:
                self.merged_pdf.save(output_path)
                self.merged_pdf.close()
                messagebox.showinfo("Descargar", f"Archivo guardado en {output_path}.")
            except Exception as e:
                messagebox.showerror("Error", f"No se pudo guardar el archivo: {e}")

# Crear ventana de Tkinter
root = tk.Tk()
app = PDFMergerApp(root)
root.mainloop()
