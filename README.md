# Projeto-Snake
Game feito a partir de um tutorial

>>SNAKE

public class Snake : MonoBehaviour {

    // movimentar sempre para o padrao: direita
    Vector2 dir = Vector2.right;

    // snake comeu alguma coisa?
    bool eat = false;

    void Start()
    {
        // mover a cobra sempre com 200ms
        InvokeRepeating("move", 0.2f, 0.2f);
    }

    void Update()
    {
        // movimentar a snake
        if (Input.GetKey(KeyCode.RightArrow))
            dir = Vector2.right;
        else if (Input.GetKey(KeyCode.DownArrow))
            dir = -Vector2.up;
        else if (Input.GetKey(KeyCode.LeftArrow))
            dir = -Vector2.right;
        else if (Input.GetKey(KeyCode.UpArrow))
            dir = Vector2.up;
    }
    // quando a snake comer
    void OnTriggerEnter2D(Collider2D coll) {
        // snake comeu ?
        if (coll.name.StartsWith("foodPrefab"))
        {
            // prox movimento
            eat = true;
            // destruir a comida
            Destroy(coll.gameObject);
        }
        // colidiu?
        else { }
    }
    // movimentar
    void move() {
        //mover a cobra para uma nova direção
        transform.Translate(dir);

        // salvar a posição atual
        Vector2 v = transform.position;
    }
}

>>SPAWNFOOD

public class SpawnFood : MonoBehaviour {
    
    //acessar o prefab
    public GameObject foodPrefab;

    //Bordas
    public Transform borderTop;
    public Transform borderBottom;
    public Transform borderLeft;
    public Transform borderRight;

    //Spawn de comida
    void Spawn()
    {
        // borda esquerda e direita (pos.'x')
        int x = (int)Random.Range(borderLeft.position.x, borderRight.position.x);

        // borda topo e baixo (pos.'y')
        int y = (int)Random.Range(borderTop.position.y, borderBottom.position.y);

        // instanciar a comida com ('x','y')
        Instantiate(foodPrefab, new Vector2(x, y), Quaternion.identity); 
    }
    void Start() {
        // spawn de comida d 7', inicio em 3'
        InvokeRepeating("Spawn", 3, 7);
    }
}
