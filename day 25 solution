import java.io.File
import java.util.*
import kotlin.math.pow

var snafuString: StringBuilder = java.lang.StringBuilder()
var numToConvert: Double = 0.0
var symbols: Double = 0.0

fun main() {
    //1.READ INPUT AND SUM SNAFU-NUMBERS TO DECIMAL.
    val reader = Scanner(File("puzzleInput.txt"))
    var sumTot = 0.0
    var sumLine = 0.0

    while (reader.hasNext()) {
        val currentLine = reader.nextLine()
        for (i in currentLine.indices) {
            var temp = 0.0
            when (currentLine[i]) {
                '2' -> temp = 2 * (5.0.pow(currentLine.length - 1 - i))
                '1' -> temp = 5.0.pow(currentLine.length - 1 - i)
                '0' -> temp = 0.0
                '-' -> temp = -(5.0).pow(currentLine.length - 1 - i)
                '=' -> temp = -2 * (5.0).pow(currentLine.length - 1 - i)
            }
            sumLine += temp
        }
        sumTot += sumLine
        sumLine = 0.0
    }
    numToConvert = sumTot
    symbols = howManySymbols(sumTot)
//2. CONVERT SUM TO SNAFU.
    while (symbols > 0.0) {
        decimalToSnafu()
    }
    println(snafuString)
    //println(howManySymbols(198.0))
}

fun decimalToSnafu() {
    if (symbols == 1.0) {
        when (numToConvert) {
            0.0 -> {
                snafuString.append('0')
            }
            1.0 -> {
                snafuString.append('1')
                numToConvert -= 1
            }
            2.0 -> {
                snafuString.append('2')
                numToConvert -= 2
            }
            -1.0 -> {
                snafuString.append('-')
                numToConvert += 1
            }
            -2.0 -> {
                snafuString.append('=')
                numToConvert += 2
            }
        }
        symbols--
        return
    }
    var limit = 0.0
    for (i in 0..symbols.toInt() - 2) {
        limit += 2 * 5.0.pow(i)
    }
    if (numToConvert <= 0) {
        val temp = numToConvert * (-1)
        if (howManySymbols(temp) < symbols) {
            snafuString.append('0')
            symbols--
            return
        }
        if (numToConvert + (2 * 5.0.pow(symbols - 1)) > (-limit) &&
            numToConvert + (2 * 5.0.pow(symbols - 1)) < limit
        ) {
            snafuString.append('=')
            numToConvert += (2 * (5.0.pow(symbols - 1)))
            symbols--
            return
        } else {
            snafuString.append('-')
            numToConvert += 5.0.pow(symbols - 1)
            symbols--
            //-1103+1250= (147, 4)
            return
        }

    }

    if (howManySymbols(numToConvert) < symbols) {
        snafuString.append('0')
        symbols--
        return
    }

    if (numToConvert - (2 * 5.0.pow(symbols - 1)) > (-limit) &&
        numToConvert - (2 * 5.0.pow(symbols - 1)) < limit
    ) {
        snafuString.append('2')
        numToConvert -= 2 * (5.0.pow(symbols - 1))
        symbols--
        //2022-3125= (-1103, 5)
        //147-125= (22, 3)
        //22-25=(-3,2)
        return
    } else {
        snafuString.append('1')
        numToConvert -= 5.0.pow(symbols - 1)
        symbols--
        return
    }
}

fun howManySymbols(myNum: Double): Double {
    var count = 0.0
    var m = 0.0
    for (i in 0..20) {
        if (myNum > 2 * 5.0.pow(i) + m) {
            m = 2 * 5.0.pow(i)
        } else {
            count = i + 1.0
            break
        }
    }
    return count
}

