# Lab-1-Free-Fall
This Laboratory explores how objects fall under constant acceleration.
public class DropFreeFall : MonoBehaviour
{

    public Rigidbody m_rigidbody;
    public GameObject m_sphereImage;
    float timer = 0.0f;  // Timer to track time
    public float dTime = 0.1f;
    bool flag=false;

    public bool force = false;
    bool flagKeyPressed = false;

    public bool buttomPressedDebug = false;


    // Update is called once per frame
    void Update()
    {
        if (OVRInput.GetDown(OVRInput.Button.One) ||  buttomPressedDebug ) // Activate gravity, sphere starts to drop
        {
                m_rigidbody.useGravity = true; 
                                  flag = true;
                        flagKeyPressed = true;
        }
    }


    void OnCollisionEnter(Collision collision)
    {
        flag = false;
        Debug.Log("flag");
    }

    private void FixedUpdate()
    {

        if (flag)
        {
            timer += Time.deltaTime;       // clock starts to count every second that passes

            // Check if one second has passed
            if (timer >= dTime)
            {
                GameObject sphereImage = Instantiate(m_sphereImage, m_rigidbody.transform.position, m_rigidbody.transform.rotation);
                // Reset the timer
                timer = 0.0f;
            }

        }


        if (force && flagKeyPressed)
        {
            //Use Acceleration as the force on the Rigidbody
            m_rigidbody.AddForce(1.0f*Vector3.right, ForceMode.Impulse);
            flagKeyPressed = false;

        }
    }




    



}
