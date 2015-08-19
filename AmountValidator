package primeface;

import java.math.BigDecimal;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

import javax.faces.application.FacesMessage;
import javax.faces.component.UIComponent;
import javax.faces.context.FacesContext;
import javax.faces.validator.FacesValidator;
import javax.faces.validator.Validator;
import javax.faces.validator.ValidatorException;

@FacesValidator("test.amtValidator")
public class AmountValidator implements Validator {

	private static final String AMT_PATTERN = "^[&amp;]{0,9}\\d{0,9}(,\\d+)*(\\.\\d{0,2})?$";

	private Pattern pattern;
	private Matcher matcher;

	public AmountValidator() {
		pattern = Pattern.compile(AMT_PATTERN);
	}

	/**
	 * 
	 * 
	 * 
	 <code>
	 1.-ve values not allowed 
	 2. <dot> . not allowed 
	 3. float format allowed
	 4. not allowed chars
	 </code>
	 */
	@Override
	public void validate(FacesContext context, UIComponent component,
			Object value) throws ValidatorException {

		if (value != null) {
			if (value.equals(".")) {
				FacesMessage msg = new FacesMessage(
						"Amount validation failed.",
						"Invalid amount format -2 <dot not allowed> .");
				msg.setSeverity(FacesMessage.SEVERITY_ERROR);
				throw new ValidatorException(msg);
			} else {
				matcher = pattern.matcher(value.toString());
				if (!matcher.matches()) {
					FacesMessage msg = new FacesMessage(
							"Amount validation failed.",
							"Invalid amount format -3,4 <only allow digits and dots >.");
					msg.setSeverity(FacesMessage.SEVERITY_ERROR);
					throw new ValidatorException(msg);
				} else if (new BigDecimal(value.toString()).doubleValue() < 0) {
					FacesMessage msg = new FacesMessage(
							"Amount validation failed.",
							"Invalid amount format -1 <Negative Value cab't be accpeted> .");
					msg.setSeverity(FacesMessage.SEVERITY_ERROR);
					throw new ValidatorException(msg);
				}
			}
		}
	}
}
