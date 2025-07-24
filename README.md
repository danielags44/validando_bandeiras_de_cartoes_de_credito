# validando_bandeiras_de_cartoes_de_credito
Utilizando o Github copilot como auxiliador para a criação de um código que valide bandeiras de cartão de crédito com base em seus números.


/**
 * Validates a credit card number and determines its flag (bandeira).
 * @param {string} cardNumber - The credit card number as a string.
 * @returns {{ valid: boolean, bandeira: string|null }}
 */
function validateCreditCard(cardNumber) {
    // Remove spaces and dashes
    const sanitized = cardNumber.replace(/\D/g, '');
    let bandeira = null;

    // Visa: starts with 4
    if (/^4/.test(sanitized)) {
        bandeira = 'Visa';
    }
    // MasterCard: 51-55 or 2221-2720
    else if (/^(5[1-5])/.test(sanitized) || /^(222[1-9]|22[3-9][0-9]|2[3-6][0-9]{2}|27[01][0-9]|2720)/.test(sanitized)) {
        bandeira = 'MasterCard';
    }
    // Elo: 4011, 4312, 4389, 4514, 4576, 5041, 5066, 5067, 509, 6277, 6362, 6363
    else if (/^(4011|4312|4389|4514|4576|5041|5066|5067|509|6277|6362|6363)/.test(sanitized)) {
        bandeira = 'Elo';
    }
    // American Express: 34 or 37
    else if (/^(34|37)/.test(sanitized)) {
        bandeira = 'American Express';
    }
    // Discover: 6011, 65, 644-649
    else if (/^(6011|65|64[4-9])/.test(sanitized)) {
        bandeira = 'Discover';
    }
    // Hipercard: 6062
    else if (/^6062/.test(sanitized)) {
        bandeira = 'Hipercard';
    }

    // Luhn algorithm for card validation
    function luhnCheck(num) {
        let sum = 0;
        let shouldDouble = false;
        for (let i = num.length - 1; i >= 0; i--) {
            let digit = parseInt(num.charAt(i), 10);
            if (shouldDouble) {
                digit *= 2;
                if (digit > 9) digit -= 9;
            }
            sum += digit;
            shouldDouble = !shouldDouble;
        }
        return sum % 10 === 0;
    }

    const valid = luhnCheck(sanitized) && bandeira !== null;
    return { valid, bandeira };
}



Utlizei dados fornecidos pelo curso da DIO, quaisquer números utilizados foram totalmente fictícios, não pertencendo a nenhuma pessoa específica. Trabalho realizado com o apoio do "4Devs" para auxílio dos números obtidos.
