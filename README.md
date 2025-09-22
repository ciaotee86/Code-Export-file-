import android.content.Context
import java.io.File
import java.io.FileWriter
import java.io.BufferedWriter

data class User(val id: Int, val name: String, val email: String)

fun exportUsersToCsv(context: Context, users: List<User>): File? {
    return try {
        val dir = context.getExternalFilesDir(null)
        val file = File(dir, "users.csv")
        val writer = BufferedWriter(FileWriter(file))

      
        writer.write("ID,Name,Email")
        writer.newLine()

        
        for (u in users) {
            writer.write("${u.id},${u.name},${u.email}")
            writer.newLine()
        }

        writer.flush()
        writer.close()
        file
    } catch (e: Exception) {
        e.printStackTrace()
        null
    }
}
