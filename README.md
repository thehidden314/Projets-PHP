# Projets-PHP_______Création d'un formulaire de contact_________
#_____Fichier_PHP(index.php)_______
<?php
    $firstname = $name = $email = $phone = $message = "";
    $firstnameError = $nameError = $emailError = $phoneError = $messageError = ""; #Validation coté server

    if ($_SERVER["REQUEST_METHOD"] == "POST"){
        $firstname = verifyInput($_POST["firstname"]);
        $name = verifyInput($_POST["name"]);
        $email = verifyInput($_POST["email"]);
        $phone = verifyInput($_POST["phone"]);
        $message = verifyInput($_POST["message"]);
        if(empty($firstname))
        {
            $firstnameError = "Je veux connaitre ton prénom !";
        }
        if(empty($name))
        {
            $nameError = "Et oui, je veux tout savoir. Même ton nom !";
        }
        if(isPhone($phone)) #Validation_téléphone

        {
            $phoneError = "Je veux connaitre ton numèro de téléphone !";
        }
        if(empty($message))
        {
            $messageError = "Qu'est-ce que tu veux me dire ?";
        }
        if(!isEmail($email)) #Validation_email
        {
            $emailError = "T'essaies de me rouler? C'est pas un email ça !";
        }
    }
    function isEmail($var) #Validation_email
    {
        return filter_var($var, FILTER_VALIDATE_EMAIL);
    }
    function verifyInput($var)
    {
        $var = trim($var);
        $var = stripslashes($var);
        $var = htmlspecialchars($var);
        return $var;
    }
    function isPhone($var)
    {
        return preg_match("/^[0-9 ]*$/", $var);
    }
?>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Contactez-moi</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <!-- Latest compiled and minified CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.4.1/dist/css/bootstrap.min.css" >
    <!-- Latest compiled and minified JavaScript -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@3.4.1/dist/js/bootstrap.min.js"></script>
    <link href="https://fonts.googleapis.com/css?family=Lato" type="text/css" rel="stylesheet">
    <link rel="stylesheet" href="css/style.css">
    
</head>
<body>
    <div class="container">
        <div class="divider"></div>
        <div class="heading">
            <h2>Contactez-moi</h2>
        </div>
        <div class="row">
            <div class="col-lg-10 col-lg-offset-1">
                <form id="contact-form" method="post" role="form" action="<?php echo htmlspecialchars($_SERVER['PHP_SELF']); ?>">
                    <div class="row">
                        <div class="col-md-6">
                            <label for="firstname">Prénom<span class="blue"> *</span></label>
                            <input type="text" id="firstname" name="firstname" class="form-control" placeholder="Écrire ton prénom" value="<?php echo $firstname; ?>">
                            <p class="comments"><?php echo $firstnameError; ?></p>
                        </div>
                        <div class="col-md-6">
                            <label for="name">Nom<span class="blue"> *</span></label>
                            <input type="text" id="name" name="name" class="form-control" placeholder="Écrire ton nom" value="<?php echo $name; ?>">
                            <p class="comments"><?php echo $nameError; ?></p>
                        </div>
                        <div class="col-md-6">
                            <label for="email">Email<span class="blue"> *</span></label>
                            <input type="email" id="email" name="email" class="form-control" placeholder="Votre email" value="<?php echo $email; ?>">
                            <p class="comments"><?php echo $emailError; ?></p>
                        </div>
                        <div class="col-md-6">
                            <label for="phone">Téléphone</label>
                            <input type="tel" id="phone" name="phone" class="form-control" placeholder="Votre numèro de téléphone" value="<?php echo $phone; ?>">
                            <p class="comments"><?php echo $phoneError; ?></p>
                        </div>
                        <div class="col-md-12">
                            <label for="message">Message<span class="blue"> *</span></label>
                            <textarea type="text" id="message" name="message" class="form-control" placeholder="Votre nom" rows="4"><?php echo $message; ?></textarea>
                            <p class="comments"><?php echo $messageError; ?></p>
                        </div>
                        <div class="col-md-12">
                            <p class="blue"><strong>* Ces informations sont requises !</strong></p>
                        </div>
                        <div class="col-md-12">
                            <input type="submit" class="button1" value="Envoyer">
                        </div>
                    </div>
                    <p class="thank-you">Votre message a bien été envoyé. Merci de m'avoir contacté :)</p>
                </form>
            </div>
        </div>
    </div>
</body>
</html>
#______Fichier_CSS(style.css)_______
body
{
    font-family: "Lato" , sans-serif;
    margin: 70px 0px;
    background: #0069d6;
}
.divider
{
    width: 100px;
    height: 2px;
    background: #ffa500;
    margin: 0 auto;
}
.heading
{
    text-align: center;
    margin-bottom: 60px;
}
h2
{
    text-transform: uppercase;
    font-weight: bold;
    color: #fff;
}
#contact-form
{
    font-size: 20px;
    background: #fff;
    padding: 40px;
    border-radius: 10px;

}
.blue
{
    color: #0069d6;
}
.form-control
{
    height: 50px;
    font-size: 18px;
}
.comments
{
    font-style: italic;
    font-size: 18px;
    color: #d82c2e;
    height: 25px;
}
#contact-form input[type=submit]
{
    margin: 40px auto 0px;
    display: block;
}
.button1
{
    border: 1px solid #ddd;
    background: #ffa500;
    color: #fff;
    width: 100%;
    font-weight: bold;
    text-transform: uppercase;
    padding: 18px;
    border-radius: 5px;
    transition: all 0.3s ease-in 0s;
}
.button1:hover
{
    background: #0c0c0c;
}
.thank-you
{
    text-align: center;
    margin-top: 15px;
    font-weight: bold;
    font-size: 22px;
}
