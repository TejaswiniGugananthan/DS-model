```
1.Rotating the ball
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class exp1 : MonoBehaviour
{
    void Start()
    {
    }
    void Update()
    {
        transform.RotateAround(Vector3.right, Vector3.up, 60 * Time.deltaTime);
    }
}

2.Roll a ball
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class balls : MonoBehaviour
{
    float XForce = 5.0f;
    float zForce = 20.0f;
    float yForce = 10.0f;
    void Start()
    {   
    }
    void Update()
    {
        float x = 0.0f, y = 0.0f, z = 0.0f;
        if(Input.GetKey(KeyCode.A))
        {
            x = x - XForce;
        }
        if (Input.GetKey(KeyCode.D))
        {
            x = x + XForce;
        }
        if (Input.GetKey(KeyCode.W))
        {
            z = z - zForce;
        }
        if (Input.GetKey(KeyCode.S))
        {
            z = z + zForce;
        }
        if (Input.GetKey(KeyCode.Space))
        {
            y = yForce;
        }
        GetComponent<Rigidbody>().AddForce(x, y, z);
    }
}

3.Pingpong
GameManager:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class GameManager : MonoBehaviour
{
    public Ball ball;
    public Paddle paddle;
    public static Vector2 bottomLeft;
    public static Vector2 topRight;
    void Start()
    {
        bottomLeft = Camera.main.ScreenToWorldPoint(new Vector2(0, 0));
        topRight = Camera.main.ScreenToWorldPoint(new Vector2(Screen.width, Screen.height));
        Instantiate(ball);
        Paddle paddle1 = Instantiate(paddle) as Paddle;
        Paddle paddle2 = Instantiate(paddle) as Paddle;
        paddle1.Init(true);
        paddle2.Init(false);
    }
    void Update()
    {

    }
}
Paddle:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class Paddle : MonoBehaviour
{
    [SerializeField]
    float speed;
    float height;
    string input;
    public bool isRight;
    void Start()
    {
        height = transform.localScale.y;
        speed = 6f;
    }
    public void Init(bool isRightPaddle)
    {
        isRight = isRightPaddle;
        Vector2 pos = Vector2.zero;
        if (isRight)
        {
            pos = new Vector2(GameManager.topRight.x, 0);
            pos -= Vector2.right * transform.localScale.x*5;
            input = "PaddleRight";
        }
        else
        {
            pos = new Vector2(GameManager.bottomLeft.x, 0);
            pos += Vector2.right * transform.localScale.x*5;
            input = "PaddleLeft";
        }
        transform.position = pos;
        transform.name = input;
    }
    void Update()
    {
        float move = Input.GetAxis(input) * Time.deltaTime * speed;
        if (transform.position.y < GameManager.bottomLeft.y + height / 2 && move < 0)
        {
            move = 0;
        }
        if (transform.position.y > GameManager.topRight.y - height / 2 && move > 0)
        {
            move = 0;
        }
        transform.Translate(move * Vector2.up);
    }
}
Ball:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class Ball : MonoBehaviour
{
    [SerializeField]
    float speed;
    float radius;
    Vector2 direction;
    void Start()
    {
        direction = Vector2.one.normalized;
        radius = transform.localScale.x / 2;
    }
    void Update()
    {
        transform.Translate(direction * speed * Time.deltaTime);
        if (transform.position.y < GameManager.bottomLeft.y + radius && direction.y < 0)
        {
            direction.y = -direction.y;
        }
        if (transform.position.y > GameManager.topRight.y - radius && direction.y > 0)
        {
            direction.y = -direction.y;
        }
        if (transform.position.x < GameManager.bottomLeft.x + radius && direction.x < 0)
        {
            Debug.Log("Right Player win");
            Time.timeScale = 0;
        }
        if (transform.position.x > GameManager.topRight.x - radius && direction.x > 0)
        {
            Debug.Log("Left Player win");
            Time.timeScale = 0;
        }
    }
    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.tag == "Paddle")
        {
            bool isRight = other.GetComponent<Paddle>().isRight;
            if (isRight == true && direction.x > 0)
            {
                direction.x = -direction.x;
            }
            if (isRight == false && direction.x < 0)
            {
                direction.x = -direction.x;
            }
        }
    }
}

4.Animal phase I:
PlayerController:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class planecontroller : MonoBehaviour
{
    public float horizontalInput;
    public float speed = 10.0f;
    public float xRange = 10f;
    public GameObject projectilePrefab;
    void Start()
    {
    }
    void Update()
    {
        if(transform.position.x < -xRange)
        {
            transform.position = new Vector3(-xRange, transform.position.y, transform.position.z);
        }
        if(transform.position.x>xRange)
        {
            transform.position = new Vector3(xRange, transform.position.y, transform.position.z);
        }
        horizontalInput = Input.GetAxis("Horizontal");
        transform.Translate(Vector3.right * horizontalInput * Time.deltaTime * speed);
        if(Input.GetKeyDown(KeyCode.Space))
        {
            Instantiate(projectilePrefab, transform.position, projectilePrefab.transform.rotation);
        }
    }
}
MoveForward:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class moveforward : MonoBehaviour
{
    public float speed = 40.0f;
    void Start()
    {   
    }
    void Update()
    {
        transform.Translate(Vector3.forward * Time.deltaTime * speed);
    }
}

5.Animal phase II
SpawmManager:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class SpamManager : MonoBehaviour
{
    public GameObject[] animalPrefabs;
    private float spamRangeX = 20;
    private float spamPosZ = 20;
    private float startDelay = 2;
    private float spamInterval = 1.5f;
    void Start()
    {
        InvokeRepeating("SpamRandomAnimal", startDelay, spamInterval);
    }
    void Update()
    {
        
    }
    void SpamRandomAnimal()
    {
        int animalIndex = Random.Range(0, animalPrefabs.Length);
        Vector3 spamPos = new Vector3(Random.Range(-spamRangeX, spamRangeX), 0, spamPosZ);
        Instantiate(animalPrefabs[animalIndex], spamPos, animalPrefabs[animalIndex].transform.rotation);
    }
}
DetectionCollision:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class DetectCollider : MonoBehaviour
{
    void Start()
    {
    }
    void Update()
    {
    }
    private void OnTriggerEnter(Collider other)
    {
        Destroy(gameObject);
        Destroy(other.gameObject);
    }
}

6.Animator:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class exp6 : MonoBehaviour
{
    public Animator animator;
    public float InputX;
    public float InputY;
    void Start()
    {
        animator = this.gameObject.GetComponent<Animator>();
    }
    void Update()
    {
        InputX = Input.GetAxis("Horizontal");
        InputY = Input.GetAxis("Vertical");
        animator.SetFloat("InputX", InputX);
        animator.SetFloat("InputY", InputY);
    }
}

7.Redirecting the scene:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;
public class player : MonoBehaviour
{
    public GameObject WinText;
    Rigidbody rb;
    public void start()
    {
        rb = GetComponent<Rigidbody>();
    }
    public void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
            SceneManager.LoadScene("scene");
    }
    private void OnMouseDown()
    {
        Destroy(gameObject);
    }
    public void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.tag == "sphere")
        {
            Destroy(collision.gameObject);
            WinText.SetActive(true);
        }
    }
}

