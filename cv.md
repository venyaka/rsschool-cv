# Veniamin Ilkov
## My contacts:

__Mobile-Phone:__ +7 771 535 3963

__e-mail:__ [ilkovveniamin@gmail.com](mailto:ilkovveniamin@gmail.com)

## About Me
I have been programming for several years, I have a little experience of teamwork on a common project and also twice won a prize in a programming hackathon from the Step Academy.
I'm learning fast.

## Skills:
* HTML/CSS
* Javascript
* C/C++ for microcontrollers
* C++
* Java
* Spring
* Python
* Git

## Code examples:
This is an excerpt from the online wallet user service , written by me using java and spring boot.
```java

@Service
@RequiredArgsConstructor
@Slf4j
public class UserService {

    private final UserRepository userRepository;

    public boolean signIn(String phone) {
        PhoneValidator phoneValidator = new PhoneValidator();
        if (phoneValidator.isValidPhoneNumber(phone)) {
            User userFromDB = userRepository.findByPhone(phone);
            User newuser = new User();

            if (userFromDB == null) {
                newuser.setPhone(phone);

                SecureRandom random = new SecureRandom();
                String randomCode = new BigInteger(12, random).toString(64);
                newuser.setVerificationCode(randomCode);
                newuser.setEnabled(false);
                userRepository.save(newuser);

                log.info("confirmation code: {}", randomCode);
                return true;
            }
            else {
                log.info("User with this phone-number: {} exist", phone);
            }
        }
        else {
            log.info("Uncorrected phone number: {}", phone);
        }
        return false;
    }

    public boolean confirmSignIn(PhoneCodeDto dto) {
        String code = dto.getCode();
        String phone = dto.getPhone();

        User confirmationUser = userRepository.findByPhone(phone);

        if (Objects.equals(code, confirmationUser.getVerificationCode()) && Objects.equals(phone, confirmationUser.getPhone())) {
            log.info("successful confirmation");
            confirmationUser.setEnabled(true);
            userRepository.save(confirmationUser);

            return true;
        }
        log.info("unsuccessful confirmation");
        return false;
    }


    public boolean login(PhoneDto dto) {
        String phone = dto.getPhone();
        return userRepository.existsByPhone(phone) && userRepository.findByPhone(phone).isEnabled();
    }

    public List<User> allUsers() {
        return userRepository.findAll();
    }

    public User saveUser(User user) {
        User userFromDB = userRepository.findByPhone(user.getPhone());

        if (userFromDB == null)
            return userRepository.save(user);
        return user;
    }

    public boolean deleteUser(Long userId) {
        if (userRepository.findById(userId).isPresent()) {
            userRepository.deleteById(userId);
            return true;
        }
        return false;
    }

    public List<User> findAll() {
        return userRepository.findAll();
    }
}
```

## Experience:
* A simple example of an online walletю
* telegram bot for playing the game "words", and communicating with him.
* Arduino projects:
  * remote control of the computer via the remote control (mouse, keyboard, media) via a microcontroller connected via Usb
  * modification of lighting in the apartment for remote control
* A program that changes slides for another program

## English
I am studying English at Karaganda Technical University. My current level is A2 (Pre-Intermediate).
