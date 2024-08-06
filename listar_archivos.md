```bash
# ~/.bashrc

# Función para listar archivos con una extensión específica
listar_archivos() {
    local extension="$1"
    if [[ -z "$extension" ]]; then
        echo "Por favor, proporciona una extensión de archivo (por ejemplo, .mp4)"
        return 1
    fi

    find . -type f -name "*${extension}" 2>/dev/null | while IFS= read -r file; do
        echo "Found file: $file"
    done
}
```