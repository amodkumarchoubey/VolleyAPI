# VolleyAPI


•	Automatic scheduling of network requests.




•	It is developed by google.





•	Multiple concurrent network connections.


•	Transparent disk and memory response caching with standard HTTP cache coherence.





•	Support for request prioritization.



•	Cancellation request API. You can cancel a single request, or you can set blocks or scopes of requests to cancel.


•	Ease of customization, for example, for retry and back off.


•	Strong ordering that makes it easy to correctly populate your UI with data fetched asynchronously from the network.


•	Debugging and tracing tools.

Volley is not suitable for large download or streaming operations since Volley holds all responses in memory during parsing .









```

package volleyapi.com.volleyapi;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

import com.android.volley.Request;
import com.android.volley.RequestQueue;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.StringRequest;
import com.android.volley.toolbox.Volley;

public class MainActivity extends AppCompatActivity {

    private Button btnRequest;

    private RequestQueue mRequestQueue;
    private StringRequest mStringRequest;
    private String url = "https://jsonplaceholder.typicode.com/posts";
    TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnRequest = (Button) findViewById(R.id.buttonRequest);
        textView = (TextView) findViewById(R.id.txt_respo);
        btnRequest.setOnClickListener(new View.OnClickListener() {
                                          @Override
                                          public void onClick(View v) {

                                              call_VolleyApi();

                                          }
                                      }

        );

    }

    private void call_VolleyApi() {

        //RequestQueue initialized
        mRequestQueue = Volley.newRequestQueue(this);

        //String Request initialized
        mStringRequest = new StringRequest(Request.Method.GET, url, new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {


                textView.setText(response.toString());

            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {

                Toast.makeText(getApplicationContext(), "Error  is :" + error.toString(), Toast.LENGTH_LONG).show();//display the response on screen

            }
        });

        mRequestQueue.add(mStringRequest);
    }


}
```
