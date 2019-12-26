

import java.util.ArrayList;
import java.util.List;

import org.springframework.http.HttpHeaders;
import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.reactive.function.BodyInserter;
import org.springframework.web.reactive.function.BodyInserters;
import org.springframework.web.reactive.function.client.WebClient;

import com.sample.model.DentalClaim;

import reactor.core.publisher.Mono;
@RestController
@RequestMapping(value="/samController")
public class SampleController {

	@RequestMapping(value="/details",method=RequestMethod.GET)
	public String sampleTest(){
		DentalClaim dc=new DentalClaim();
		List<Integer> list=new ArrayList<>();
		list.add(5551);
		list.add(5552);
		list.add(5553);
		dc.setClmSeqNum(4444);
		dc.setClmLnSeqNum(list);
		/*dc.setDcn("DC24232lj");
		dc.setDcnSplitNum("3");*/
		try{
		Mono<DentalClaim> tt=WebClient.builder().baseUrl("http://localhost:8082/controller/details")
		.build()
		.post()
		.body(BodyInserters.fromValue(dc))
		.header(HttpHeaders.CONTENT_TYPE, MediaType.APPLICATION_JSON_VALUE)
		.accept(MediaType.APPLICATION_JSON)
		.exchange()
		.block()
		.bodyToMono(DentalClaim.class);
		 
		System.out.println(" ====> "+tt.block().getClmSeqNum());
		}catch(Exception e){
			e.printStackTrace();
		}
		
		return "Test krishna";
	}
	
}


=======================================



import java.util.ArrayList;
import java.util.List;

import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.demo.model.DentalClaim;

@RestController//(value="controller")
@RequestMapping(value="/controller")
public class DemoController {

	@RequestMapping(value="/details",
			method=RequestMethod.POST,
			consumes=MediaType.APPLICATION_JSON_VALUE,
			produces=MediaType.APPLICATION_JSON_VALUE)
	public DentalClaim  getDentalClaim(@RequestBody DentalClaim dc){
		/*DentalClaim dc=new DentalClaim();
		List<Integer> list=new ArrayList<>();
		list.add(5551);
		list.add(5552);
		list.add(5553);
		dc.setClmSeqNum(4444);
		dc.setClmLnSeqNum(list);
		System.out.println(" id ===> "+id);*/
		System.out.println("clmSeqNum "+dc.getClmSeqNum()+" ClmSeqLnNUm "+dc.getClmLnSeqNum());
		dc.setClmSeqNum(7979);
		return dc;
	}
}
