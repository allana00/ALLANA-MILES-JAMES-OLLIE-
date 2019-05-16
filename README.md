# ALLANA-MILES-JAMES-OLLIE-

10 RIDDLES

**1)I'm tall when I'm young and I'm short when I'm old. What am I?**
A candle

**2)What has an eye but can not see?**
A needle

**3)If you have me, you want to share me. If you share me, you haven't got me. What am I?**
A secret

**4)I am never thirsty but always drinking. What am I?**
A fish

**5)Give me food, and I will live. Give me water, and I will die. What am I?**
Fire.

**6)What can you hold in your left hand, but not in your right hand?**
Your right hand.

**7)The more you take away, the bigger I become. What am I?**
Hole.

**8)What goes through towns up hills but never moves?**
A road.

**9)What goes up when the rain comes down?**
Umbrella.

**10)What loses its head in the morning but gets it back at night?**
A pillow.



import UIKit

class ViewController: UIViewController {

    let questions = ["I'm tall when I'm young and I'm short when I'm old?", "What has an eye but can not see?", "If you have me, you want to share me. If you share me, you haven't got me. What am I?"]
    let answers = [["Candle", "Cow", "Peter Pan"], ["Blind Man","Needle", "iPod"],["A secret", "Food", "Water"]]
    
    //Variables
    var currentQuestion = 0
    var rightAnswerPlacement:UInt32 = 0
    var points = 0;
    
    //LabelQuestion
    
    @IBOutlet weak var label: UILabel!
    
    //Button
    @IBAction func action(_ sender: AnyObject)
    {
        if (sender.tag == Int(rightAnswerPlacement))
        {
        print ("RIGHT!!!")
        points += 1
        }
        else
    {
        print ("WRONG!!!")
        }
        
        if (currentQuestion != questions.count)
        {
        newQuestion()
        }
        else
        {
            performSegue (withIdentifier: "showScore", sender: self)
        }
    }
    
    override func viewDidAppear (_ animated: Bool)
    {
        newQuestion()
    }
    

    //Function that displays new question
    func newQuestion()
    {
        
        label.text = questions[currentQuestion]
        
        rightAnswerPlacement = arc4random_uniform(3)+1
    
    //Create a Button
        var button:UIButton = UIButton()
        
        var x = 1
        for i in 1...3
        {
            // Create a button
            button = view.viewWithTag(i) as! UIButton
            
            if (i == Int(rightAnswerPlacement))
            {
                button.setTitle(answers[currentQuestion][0], for: .normal)
            }
            else
            {
                button.setTitle(answers[currentQuestion][x], for: .normal)
                x = 2
            }
        }
            currentQuestion += 1
            
    }
    override func viewDidLoad() {
        super.viewDidLoad()
    
    }


}

This is what you need for image stuff

first add imageview to storyboard and connect it which will make that below
@IBOutlet weak var imageView: UIImageView!

@IBAction func action(_ sender: AnyObject) {
        
        imageView.image = UIImage(named: "imagename")


NEW CODE
import UIKit
import Firebase


class ViewController: UIViewController {

    @IBOutlet weak var gameOverLabel: UILabel!
    @IBOutlet weak var imageView: UIImageView!
    @IBOutlet weak var label: UILabel!
    
    
    override func viewDidLoad() {
        super.viewDidLoad()
       gameOverLabel.isHidden = true
       watch()
    }
    override func viewDidAppear (_ animated: Bool) {
        
    }
    
    
    func watch() {
        let ref = Firestore.firestore().collection("questions")
        ref.getDocuments { snapshot, error in
            for document in snapshot!.documents {
                print(document.data())
    }
       
    }
}
    
let questions = ["I'm tall when I'm young and I'm short when I'm old?", "What has an eye but can not see?", "If you have me, you want to share me. If you share me, you haven't got me. What am I?", "I am never thirsty but always drinking. What am I?", "Give me food, and I will live. Give me water, an I will die. What am I?","What can you hold in your left hand, but not in your right hand?", "The more you take away, the bigger I become. What am I?", "What goes through towns up hils but never moves?", "What goes up when the rain comes down?", "What loses its head in the morning but gets it back at night?"]
let answers = [["Candle", "Cow", "Peter Pan"], ["Needle","IPod", "Blind Man"],["A secret", "Food", "Water"],["A Fish","Flamingo", "Alcoholic"],["Fire","A Cat", "Dog having a bath"],["Your Right Hand", "Your Left Hand", "Both Hands"],["Hole", "Eating Chocolate", "My Vegetables"],["A Road", "A River", "Oxygen"],["Umbrella", "A bird", "Sea Tide"],["A Pillow", "A Tired Man", "The Moon"]]
    
    //Variables
    var currentQuestion = 0
    var rightAnswerPlacement:UInt32 = 0
    var points = 0;
    var wrongPoints = 0;
    
    func refreshView() {
        self.viewDidLoad()
        self.viewWillAppear(true)
        
    }

    //Reset Button
 @IBAction func resetButton(_ sender: Any) {
    self.refreshView()
//
//    }

    
    //Button
        func action(_ sender: AnyObject) {
        if (sender.tag == Int(rightAnswerPlacement))
        {
            
        //
        print ("RIGHT!!!")
        points += 1

        } else {
        print ("WRONG!!!")
        wrongPoints += 1
        imageView.isHidden = true

        }
        
        if (currentQuestion != questions.count)
        {
        newQuestion()
        }
        else
        {
            performSegue (withIdentifier: "showScore", sender: self)
        }
        
        if wrongPoints == 1 {
            gameOverLabel.isHidden = false
        } else {
            //carry on...
        }
    }
    

    //Function that displays new question
    func newQuestion() {
        
        label.text = questions[currentQuestion]
        
        rightAnswerPlacement = arc4random_uniform(3)+1
    
        //Create a Button
        var button:UIButton = UIButton()
        
        var x = 1
        for i in 1...3 {
            // Create a button
            button = view.viewWithTag(i) as! UIButton
            
            if (i == Int(rightAnswerPlacement))
            {
                button.setTitle(answers[currentQuestion][0], for: .normal)
            }
            else
            {
                button.setTitle(answers[currentQuestion][x], for: .normal)
                x = 2
            }
        }
            currentQuestion += 1
            
          }
     }
}
